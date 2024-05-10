

 #### 电影&&书籍

<head>
    <title>Tab Image Gallery</title>
    <style>
        .tab {
            overflow: hidden;
            border: 1px solid #ccc;
            background-color: #f1f1f1;
        }
        .tab button {
            background-color: inherit;
            float: left;
            border: none;
            outline: none;
            cursor: pointer;
            padding: 14px 16px;
            transition: 0.3s;
        }
        .tab button:hover {
            background-color: #ddd;
        }
        .tab button.active {
            background-color: #ccc;
        }
        .tabcontent {
            display: none;
            padding: 6px 12px;
            border: 1px solid #ccc;
            border-top: none;
        }
        .gallery {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }
        .gallery img {
            width: 200px;
            height: auto;
        }
    </style>
</head>
<body>

<div class="tab">
    <button class="tablinks" onclick="openCategory(event, 'Books')">书籍</button>
    <button class="tablinks" onclick="openCategory(event, 'Movies')">电影</button>
</div>

<div id="Books" class="tabcontent">
    <div class="gallery" id="booksGallery"></div>
</div>

<div id="Movies" class="tabcontent">
    <div class="gallery" id="moviesGallery"></div>
</div>

<script>
function openCategory(evt, categoryName) {
    var i, tabcontent, tablinks;
    tabcontent = document.getElementsByClassName("tabcontent");
    for (i = 0; i < tabcontent.length; i++) {
        tabcontent[i].style.display = "none";
    }
    tablinks = document.getElementsByClassName("tablinks");
    for (i = 0; i < tablinks.length; i++) {
        tablinks[i].className = tablinks[i].className.replace(" active", "");
    }
    document.getElementById(categoryName).style.display = "block";
    evt.currentTarget.className += " active";
}

// 默认打开书籍Tab
document.getElementsByClassName("tablinks")[0].click();

const filePath = './pics/sours.json'; // 确保这个路径指向你的JSON文件

fetch(filePath)
    .then(response => response.json())
    .then(data => {
        const booksGallery = document.getElementById('booksGallery');
        const moviesGallery = document.getElementById('moviesGallery');

        // 遍历书籍数据
        data.book.forEach(item => {
            const img = document.createElement('img');
            img.src = item.img;
            booksGallery.appendChild(img);
        });

        // 遍历电影数据
        data.movie.forEach(item => {
            const img = document.createElement('img');
            img.src = item.img;
            moviesGallery.appendChild(img);
        });
    })
    .catch(error => console.error('加载JSON文件时发生错误:', error));
</script>

</body>
</html>
