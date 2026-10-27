---
layout:     post
title:      "deepseek daily helper"
subtitle:   "tool structure"
date:       2026-10-27 14:4
author:     "J2Fish"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - AI
    - deepseek
    - remote service
---

just a structure

QQinfo.py
    get_openid()
    get_message() -> message:str
    prase_message_from_user(message) -> (time,content) # 调用ai解析信息
    send_message_remind(time, message) # 提醒调用这个
    send_message_talk(message) # 日常说话调用这个


storage.py
    add(time, content) -> (time, content)
    del(task_idx) -> bool:status
    search_by_content(content) -> (time, content)
    search_by_time(time) -> (time, content)# 精度到day
    revise(task_idx, r_content)
    time_to_idx(time) -> idx
    idx_to_time(task_idx) -> time
    

    idx:int 是 该条任务精确到秒的时间戳
    content:dict = (openid, task_text)
    task_text:str 是任务文本
    time:int = YYMMDDHHmmss #二十四小时制


    存储架构：
        belonging.json
            openid:[
                task1_idx, 
                task2_idx, 
                ...
            ]
        tasks.json
            tasks:{
                task1_idx: [task1_text, status],
                task2_idx: [task2_text, status],
                ...
            }
            //tasks 按idx升序排列，挂时间的时候取第一条,提醒时间精度为3分钟，提醒后status = False,未提醒的为True

reminder.py
    set_times(time, func) # 提醒区间精确到3分钟，time提供到分钟，到点即调用func