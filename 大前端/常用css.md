## 屏幕高度

```css
.tablewrap{
     height: calc(100vh - 300px);
 }
```
## 文字溢出

```css
.txt{
    width:200px;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}

```

## 多行文字

```css
.txt{
    width:200px;
    overflow: hidden
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
}
```

