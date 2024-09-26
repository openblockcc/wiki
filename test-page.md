---
title: 内部功能测试页面（不发布）
description: 
published: false
date: 2023-12-24T17:54:50.366Z
tags: 
editor: markdown
dateCreated: 2022-08-16T11:56:38.912Z
---

# 内部功能测试页面（不发布）

下方的内容演示了如何在wiki中插入商品图片并链接到对应地址。
```
<a href="https://www.baidu.com"><img src="/test/商品宣传链接图.png"></a>
```
<a href="https://www.baidu.com"><img src="/test/商品宣传链接图.png"></a>

# 渲染器示例
## 缩写
*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
The HTML specification
is maintained by the W3C.

## kroki 示例

```kroki
wavedrom

{ signal: [
  { name: "clk",         wave: "p.....|..." },
  { name: "Data",        wave: "x.345x|=.x", data: ["head", "body", "tail", "data"] },
  { name: "Request",     wave: "0.1..0|1.0" },
  {},
  { name: "Acknowledge", wave: "1.....|01." }
]}
```


```kroki
mermaid

graph TD
  A[ Anyone ] -->|Can help | B( Go to github.com/yuzutech/kroki )
  B --> C{ How to contribute? }
  C --> D[ Reporting bugs ]
  C --> E[ Sharing ideas ]
  C --> F[ Advocating ]
```


```kroki
bytefield

(defattrs :bg-green {:fill "#a0ffa0"})
(defattrs :bg-yellow {:fill "#ffffa0"})
(defattrs :bg-pink {:fill "#ffb0a0"})
(defattrs :bg-cyan {:fill "#a0fafa"})
(defattrs :bg-purple {:fill "#e4b5f7"})

(defn draw-group-label-header
  [span label]
  (draw-box (text label [:math {:font-size 12}]) {:span span :borders #{} :height 14}))

(defn draw-remotedb-header
  [kind args]
  (draw-column-headers)
  (draw-group-label-header 5 "start")
  (draw-group-label-header 5 "TxID")
  (draw-group-label-header 3 "type")
  (draw-group-label-header 2 "args")
  (draw-group-label-header 1 "tags")
  (next-row 18)

  (draw-box 0x11 :bg-green)
  (draw-box 0x872349ae [{:span 4} :bg-green])
  (draw-box 0x11 :bg-yellow)
  (draw-box (text "TxID" :math) [{:span 4} :bg-yellow])
  (draw-box 0x10 :bg-pink)
  (draw-box (hex-text kind 4 :bold) [{:span 2} :bg-pink])
  (draw-box 0x0f :bg-cyan)
  (draw-box (hex-text args 2 :bold) :bg-cyan)
  (draw-box 0x14 :bg-purple)

  (draw-box (text "0000000c" :hex [[:plain {:font-weight "light" :font-size 16}] " (12)"]) [{:span 4} :bg-purple])
  (draw-box (hex-text 6 2 :bold) [:box-first :bg-purple])
  (doseq [val [6 6 3 6 6 6 6 3]]
    (draw-box (hex-text val 2 :bold) [:box-related :bg-purple]))
  (doseq [val [0 0]]
    (draw-box val [:box-related :bg-purple]))
  (draw-box 0 [:box-last :bg-purple]))

(draw-remotedb-header 0x4702 9)

(draw-box 0x11)
(draw-box 0x2104 {:span 4})
(draw-box 0x11)
(draw-box 0 {:span 4})
(draw-box 0x11)
(draw-box (text "length" [:math] [:sub 1]) {:span 4})
(draw-box 0x14)

(draw-box (text "length" [:math] [:sub 1]) {:span 4})
(draw-gap "Cue and loop point bytes")

(draw-box nil :box-below)
(draw-box 0x11)
(draw-box 0x36 {:span 4})
(draw-box 0x11)
(draw-box (text "num" [:math] [:sub "hot"]) {:span 4})
(draw-box 0x11)
(draw-box (text "num" [:math] [:sub "cue"]) {:span 4})

(draw-box 0x11)
(draw-box (text "length" [:math] [:sub 2]) {:span 4})
(draw-box 0x14)
(draw-box (text "length" [:math] [:sub 2]) {:span 4})
(draw-gap "Unknown bytes" {:min-label-columns 6})
(draw-bottom)

```


## Diagram 示例
```diagram
PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxNDFweCIgaGVpZ2h0PSIxNzFweCIgdmlld0JveD0iLTAuNSAtMC41IDE0MSAxNzEiIGNvbnRlbnQ9IiZsdDtteGZpbGUgaG9zdD0mcXVvdDtlbWJlZC5kaWFncmFtcy5uZXQmcXVvdDsgbW9kaWZpZWQ9JnF1b3Q7MjAyMi0wOC0yMlQxNDo0Nzo1NS4wMjhaJnF1b3Q7IGFnZW50PSZxdW90OzUuMCAoV2luZG93cyBOVCAxMC4wOyBXaW42NDsgeDY0KSBBcHBsZVdlYktpdC81MzcuMzYgKEtIVE1MLCBsaWtlIEdlY2tvKSBDaHJvbWUvMTA0LjAuMC4wIFNhZmFyaS81MzcuMzYmcXVvdDsgdmVyc2lvbj0mcXVvdDsyMC4yLjYmcXVvdDsgZXRhZz0mcXVvdDtSN2FFMFJMdV9qa3dTLVhiRjI0UyZxdW90OyB0eXBlPSZxdW90O2VtYmVkJnF1b3Q7Jmd0OyZsdDtkaWFncmFtIGlkPSZxdW90O1pEeDM5LVEyOFBUY21vZGFqUGgzJnF1b3Q7IG5hbWU9JnF1b3Q756ysIDEg6aG1JnF1b3Q7Jmd0O3paUEJib1FnRUVDL2h2c0NWdTIxZHR0ZWV2TFFNNUdwa0tBWUZxdjI2NHNGVkxMZHBKY212Umg0TXdQTUF4R3R1dm5ac0VHOGFnNEtrUk9mRVgxRWhCUlo1cjRyV0R6SXk4S0Qxa2p1RWQ1QkxUOGh3Rk9nbytSd1NSS3Qxc3JLSVlXTjdudG9iTUtZTVhwSzA5NjFTbmNkV0F0WG9HNll1cVp2a2x2aGFVbUtuYitBYkVYY0dlZjNQdEt4bUJ3NnVRakc5WFJBOUl4b1piUzJmdFRORmFqVlhmVGk2NTV1UkxlREdlanRid3FJTC9oZ2FneTloWFBaSlRacjlOaHpXUE14b2crVGtCYnFnVFZyZEhLMzY1aXduUXJoc0J3WUMvUE5JK0d0VWZkQVFIZGd6ZUpTWWtFZTNJVEhnYk13bjNiVk9Qb1RCODJ4am9YYmJiZWxkd0Z1RUJ6ODdJUCtReDlsNm9QYy9aMFBOOTNmM25mczhBUFQ4eGM9Jmx0Oy9kaWFncmFtJmd0OyZsdDsvbXhmaWxlJmd0OyI+PGRlZnMvPjxnPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0icmdiKDI1NSwgMjU1LCAyNTUpIiBzdHJva2U9InJnYigwLCAwLCAwKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIwIiB5PSIxMTAiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0icmdiKDI1NSwgMjU1LCAyNTUpIiBzdHJva2U9InJnYigwLCAwLCAwKSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48L3N2Zz4=
```

## 脚注例子

### 正常脚注

Here is a footnote reference,[^1] and another.[^longnote]

[^1]: Here is the footnote.

[^longnote]: Here's one with multiple blocks.

    Subsequent paragraphs are indented to show that they
belong to the previous footnote.

### 内联脚注

Here is an inline note.^[Inlines notes are easier to write, since
you don't have to pick an identifier and move down to type the
note.]