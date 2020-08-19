---
layout: post
title: [Parsing json from terminal / command line]
date: 2020-08-19
category: ["bash"]
author: parinay.bansal
tags: [bash, shell, jq, json]
summary: Ever wondered how to parse and work with json files from a bash shell. **jq** comes to the rescue here. Using jq we can read and extract data from a json file. This tutorial is about how to read json from the bash shell and extract relevant data from it using the jq command line tool.
feature_img: 
excerpt_separator: <!--more-->
medium: 
linkedin:
facebook:
twitter:
comments: true
youtubeId: 
---

# Parsing json files from bash shell

JSON data are used for various purposes. But JSON data can’t be read easily from JSON file by using bash script like other normal files. **jq** tool is used to solve this problem. **jq** command works like **sed** and **awk** command, and it uses a domain specific language for working with JSON data. **jq** is not a built-in command. So, you have to install this command for using it. How you can install and apply **jq** command for reading or manipulating JSON data is shown in this tutorial.

## **jq installation**

Run the following command to install jq on Ubuntu.

```
$sudo apt-get install jq
```

![](https://linuxhint.com/wp-content/uploads/2018/11/1-16.png)

## **Reading JSON data**

Suppose, you have declared a JSON variable named **JsonData** in the terminal and run **jq** command with that variable to print the content of that variable.

```
$ JsonData='[{"Book":"PHP 7"}, {"Publication":"Apress"}, {"Book":"React 16 Essentials"},{"Publication":"Packt"} ]'  
$ echo ${JsonData} | jq .
```

![](https://linuxhint.com/wp-content/uploads/2018/11/2-17.png)

### **Reading JSON data with –c option**

-c option uses with jq command to print each JSON object in each line. After running the following command, each object of JsonData variable will be printed.

```
$ echo ${JsonData}| jq -c '.[]'
```

### **Reading a JSON file**

jq command can be used for reading JSON file also. Create a JSON file named Students.json with the following content to test the next commands of this tutorial.

#### **Students.json**

```
[
    {
        "roll" : 3,
        "name": "Micheal",
        "batch": 29,
        "department": "CSE"
    },
    {
        "roll": 55,
        "name": "Lisa",
        "batch": 34,
        "department": "BBA"
    },
    {
        "roll": 12,
        "name": "John"
        "batch" : 22,
        "department": "English"
    }
]
```

Run the following command to read Students.json file.

```
$ jq ‘.’ Students.json
```

![](https://linuxhint.com/wp-content/uploads/2018/11/4-17.png)

### **Reading JSON file with ‘|’**

You can use ‘|’ symbol in the following way to read any JSON file.

```
$ cat Students.json | jq '.'
```

![](https://linuxhint.com/wp-content/uploads/2018/11/5-16.png)

### **Reading single key values**

You can easily read any particular object from a JSON file by using **jq** command. In **Students.json**, there are four objects. These are **roll, name, batch, and department**. If you want to read the value of **department** key only from each record then run **jq** command in the following way.

```
$ jq '.[] | .department' Students.json
```
![](https://linuxhint.com/wp-content/uploads/2018/11/6-15.png)

### **Reading multiple keys**

If you want to read two or more object values from JSON data then mention the object names by separating comma (,) in the jq command. The following command will retrieve the values of **name** and **department** keys.

```
$ jq '.[] | .name, .department' Students.json
```
![](https://linuxhint.com/wp-content/uploads/2018/11/7-16.png)

### **Remove key from JSON data**

**jq** command is used not only for reading JSON data but also to display data by removing the particular key. The following command will print all key values of **Students.json** file by excluding **batch** key. **map** and **del** function are used in **jq** command to do the task.

```
$ jq 'map(del(.batch))' Students.json
```

![](https://linuxhint.com/wp-content/uploads/2018/11/8-13.png)

### **Mapping Values**

Without deleting the key from JSON data, you can use map function with jq command for various purposes. Numeric values of JSON data can be increased or decreased by map function. Create a JSON file named **Number.json** with the following content to test the next commands.

```
[ 40,34,12,67,45]
```
Run the following command to add 10 with each object value of **Numbers,json**.

```
$ jq 'map(.+10)' Numbers.json
```

![](https://linuxhint.com/wp-content/uploads/2018/11/9-14.png)

Run the following command to subtract 10 from each object value of **Numbers,json**.

```
$ jq 'map(.-10)' Numbers.json
```
![](https://linuxhint.com/wp-content/uploads/2018/11/10-12.png)

### **Searching values by index and length**

You can read objects from JSON file by specifying the particular index and length. Create a JSON file named **colors.json** with the following data.

```
["Red","Green","Blue","Yellow","Purple"]
```

Run the following command to read two values starting from the third index of colors.json file.

```
$ jq '.[2:4]' colors.json
```

![](https://linuxhint.com/wp-content/uploads/2018/11/11-12.png)

You can specify the length or starting index to read data from JSON file. In the following example, the number of data value is given only. In this case, the command will read four data from the first index of colors.json.

```
$ jq '.[:4]' colors.json
```

![](https://linuxhint.com/wp-content/uploads/2018/11/12-14.png)

You can specify the starting point only without any length value in **jq** command and the value can be positive or negative. If the starting point is positive then the index will count from the left side of the list and starting from zero. If the starting point is negative then the index will count from the right side of the list and starting from one. In the following example, the starting point is -3\. So, the last three values from the data will display.

```
$ jq '.[-3:]' colors.json
```

![](https://linuxhint.com/wp-content/uploads/2018/11/13-11.png)

When you will work with JSON data and want to parse or manipulate data according to your requirements then jq command will help you to make your task easier.