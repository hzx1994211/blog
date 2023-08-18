
```js
##二进制转utf-8
//设置缓冲器
let reader = new FileReader()
//转换成utf-8
reader.readAsText(response.data, "utf-8")
reader.onload = () => {
  let msgInfo = JSON.parse(reader.result)
}


##用文件流下载文件（ Blob）时各种类型文件的 type 整理
拓展名	文件类型	MIME类型
.aac	AAC 音频	audio/aac
.abw	AbiWord 文档	application/x-abiword
.arc	存档文档(多个文件嵌入)	application/x-freearc
.avi	AVI: 音频视频交错	video/x-msvideo
.azw	亚马逊Kindle电子书格式	application/vnd.amazon.ebook
.bin	任何类型的二进制数据	application/octet-stream
.bmp	Windows OS/2位图图形	image/bmp
.bz	BZip 存档	application/x-bzip
.bz2	BZip2 存档	application/x-bzip2
.csh	C-Shell 脚本	application/x-csh
.css	CSS	text/css
.csv	CSV	text/csv
.doc	Microsoft Word	application/msword
.docx	Microsoft Word (OpenXML)	application/vnd.openxmlformats-officedocument.wordprocessingml.document
.eot	MS嵌入式OpenType字体	application/vnd.ms-fontobject
.epub	电子出版物(EPUB)	application/epub+zip
.gif	GIF	image/gif
.htm	超文本标记语言 (HTML)	text/html
.html	超文本标记语言 (HTML)	text/html
.ico	Icon 格式	image/vnd.microsoft.icon
.ics	iCalendar 格式	text/calendar
.jar	Java Archive (JAR)	application/java-archive
.jpeg	JPEG 图片	image/jpeg
.jpg	JPEG 图片	image/jpeg
.js	JavaScript	text/javascript
.json	JSON 格式	application/json
.jsonld	JSON-LD 格式	application/ld+json
.mid	乐器数字接口(MIDI)	audio/midi audio/x-midi
.midi	乐器数字接口(MIDI)	audio/midi audio/x-midi
.mjs	JavaScript 模块	text/javascript
.mp3	MP3 音频	audio/mpeg
.mpeg	MPEG 视频	video/mpeg
.mpkg	苹果安装程序包	application/vnd.apple.installer+xml
.odp	OpenDocument演示文档	application/vnd.oasis.opendocument.presentation
.ods	OpenDocument 电子表格文件	application/vnd.oasis.opendocument.spreadsheet
.odt	OpenDocument 文本文档	application/vnd.oasis.opendocument.text
.oga	OGG 音频	audio/ogg
.ogv	OGG 视频	video/ogg
.ogx	OGG	application/ogg
.otf	OpenType 字体	font/otf
.png	便携式网络图形（PNG）	image/png
.pdf	PDF	application/pdf
.ppt	Microsoft PowerPoint	application/vnd.ms-powerpoint
.pptx	Microsoft PowerPoint (OpenXML)	application/vnd.openxmlformats-officedocument.presentationml.presentation
.rar	RAR 存档	application/x-rar-compressed
.rtf	富文本格式 (RTF)	application/rtf
.sh	Bourne shell 脚本	application/x-sh
.svg	可缩放矢量图形 (SVG)	image/svg+xml
.swf	小型web格式 (SWF) or Adobe Flash document	application/x-shockwave-flash
.tar	Tape 归档(TAR)	application/x-tar
.tif	标记图像文件格式 (TIFF)	image/tiff
.tiff	Tagged Image File Format (TIFF)	image/tiff
.ttf	TrueType 字体	font/ttf
.txt	Text	text/plain
.vsd	Microsoft Visio	application/vnd.visio
.wav	波形音频格式	audio/wav
.weba	WEBM 音频	audio/webm
.webm	WEBM 视频	video/webm
.webp	WEBP 图片	image/webp
.woff	网页开放字体格式 (WOFF)	font/woff
.woff2	网页开放字体格式 (WOFF)	font/woff2
.xhtml	XHTML	application/xhtml+xml
.xls	Microsoft Excel	application/vnd.ms-excel
.xlsx	Microsoft Excel (OpenXML)	application/vnd.openxmlformats-officedocument.spreadsheetml.sheet
.xml	XML	application/xml（普通用户不可读）、text/xml（普通用户可读）
.xul	XUL	application/vnd.mozilla.xul+xml
.zip	ZIP	application/zip
.3gp	3GPP audio/video 容器	video/3gpp、audio/3gpp（不含视频）
.3g2	3GPP2 audio/video 容器	video/3gpp2、audio/3gpp2（不含视频）
.7z	7-zip	application/x-7z-compressed


##js实现table表格拖拽改变列宽
https://github.com/uso51984/resizable-columns-table


js 金额转千分位
/**
* 金额转千分位
* @param num => 1243250.00
* @return 1,243,250
*/
export function formatWithRegex (num: number | string) {
// 就是说1-3位后面一定要匹配3位
return !(num + '').includes('.')
? (num + '').replace(/\d{1,3}(?=(\d{3})+$)/g, (match) => {
return match + ','
})
: (num + '').replace(/\d{1,3}(?=(\d{3})+(\.))/g, (match) => {
return match + ','
})
}


##深拷贝
const judgeType = origin => {
return Object.prototype.toString.call(origin).replaceAll(new RegExp(/\[|\]|object /g), "");
};
const reference = ["Set", "WeakSet", "Map", "WeakMap", "RegExp", "Date", "Error"];
function deepClone(obj) {
// 定义新的对象，最后返回
//通过 obj 的原型创建对象
const cloneObj = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj));

// 遍历对象，克隆属性
for (let key of Reflect.ownKeys(obj)) {
const val = obj[key];
const type = judgeType(val);
if (reference.includes(type)) {
newObj[key] = new val.constructor(val);
}else if (typeof val === "object" && val !== null) {
// 递归克隆
newObj[key] = deepClone(val);
}else {
// 基本数据类型和function
newObj[key] = val;
}}return newObj;
}


##将扁平化数组还原属性结构
    let jsonData = [
      { id: 1, parentId: 0, name: '一级菜单A' },
      { id: 2, parentId: 0, name: '一级菜单B' },
      { id: 3, parentId: 0, name: '一级菜单C' },
      { id: 4, parentId: 1, name: '二级菜单A-A' },
      { id: 5, parentId: 1, name: '二级菜单A-B' },
      { id: 6, parentId: 2, name: '二级菜单B-A' },
      { id: 7, parentId: 4, name: '三级菜单A-A-A' },
      { id: 8, parentId: 7, name: '四级菜单A-A-A-A' },
      { id: 9, parentId: 8, name: '五级菜单A-A-A-A-A' }
    ]
    function resetList(data) {
      let copyObj = JSON.parse(JSON.stringify(data))
      let arr = copyObj.filter(parent => {
        let filterArr = copyObj.filter(child => parent.id == child.parentId)
        filterArr.length > 0 ? (parent.child = filterArr) : (parent.child = [])
        return parent.parentId == 0
      })
      return arr
    }
    console.log(resetList(jsonData), '---jsonData')
```

