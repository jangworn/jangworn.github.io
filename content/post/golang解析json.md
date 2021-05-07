---
title: golang解析json
date: 2020-05-03 23:40:58
tags: go json struct
---

## golang解析json常用的方法有2种

### 定义struct

```
package main

import (
	"encoding/json"
	"fmt"
)

type Student struct {
	Name string `json:"Name"`
	Age  int    `json:"Age"`
	Sex  string `json:"Sex"`
}
type Class struct {
	ClassName string `json:"ClassName"`
	Students  []Student
}
type School struct {
	SchoolName string
	Id         int64 `json:"Id"`
	Class      map[string]Class
}

func main() {

	jsonData := []byte(`
    {
        "SchoolName": "Standard",
        "Class" : {
			"1": {
				"ClassName": "一年级1班",
				"Students": [
					{
						"Name":"小明",
						"Age":5,
						"Sex":"男"
					},
					{
						"Name":"小花",
						"Age":5,
						"Sex":"女"
					}
				]
			},
			"2": {
				"ClassName": "一年级2班",
				"Students": [
					{
						"Name":"小强",
						"Age":6,
						"Sex":"男"
					},
					{
						"Name":"小刚",
						"Age":5,
						"Sex":"男"
					}
				]
			}
        },
        "Id": 999
    }`)

	var s School
	err := json.Unmarshal(jsonData, &s)
	if err != nil {
		fmt.Println(err)
	}
	for _, class := range s.Class {
		fmt.Println(class.ClassName)
		for _, student := range class.Students {
			fmt.Println(student.Name, student.Age, student.Sex)
		}
	}
}


```

### 使用interface类型断言
switch 和 for要嵌套很多层
```
package main

import (
	"encoding/json"
	"fmt"
	"time"
)

func main() {

	jsonData := []byte(`
    {
        "SchoolName": "Standard",
        "Class" : {
			"1": {
				"ClassName": "一年级1班",
				"Students": [
					{
						"Name":"小明",
						"Age":5,
						"Sex":"男"
					},
					{
						"Name":"小花",
						"Age":5,
						"Sex":"女"
					}
				]
			},
			"2": {
				"ClassName": "一年级2班",
				"Students": [
					{
						"Name":"小强",
						"Age":6,
						"Sex":"男"
					},
					{
						"Name":"小刚",
						"Age":5,
						"Sex":"男"
					}
				]
			}
        },
        "Id": 999
    }`)
	var i interface{}
	json.Unmarshal(jsonData, &i)
	data := i.(map[string]interface{})
	for k, v := range data {
		switch v := v.(type) {
		case string:
			fmt.Println("string", k, v)
		case []interface{}:
			//fmt.Println("array[]", k)
			for kk, vv := range v {
				fmt.Println(kk, vv)
			}
		case map[string]interface{}:
			//fmt.Println("array[string]")
			for kk, vv := range v {
				switch vv := vv.(type) {
				case string:
					fmt.Println("string", kk, vv)
				case []interface{}:
					//fmt.Println("array[]", kk)
				case map[string]interface{}:
					//fmt.Println("array[string]", kk)
					for kkk, vvv := range vv {
						switch vvv := vvv.(type) {
						case string:
							fmt.Println("string", kkk, vvv)
						case []interface{}:
							for kkkk, vvvv := range vvv {
								switch vvvv := vvvv.(type) {
								case string:
									fmt.Println(kkkk)
								case map[string]interface{}:
									for kkkkk, vvvvv := range vvvv {
										fmt.Println(kkkkk, vvvvv)
									}
								}
							}
						default:
						}
					}
				default:
					fmt.Println(" ")
				}
			}
		default:
			fmt.Println(k, v)
		}
	}
	fmt.Println(time.Now())

}
```