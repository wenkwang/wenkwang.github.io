---
layout: page
title: Images
---
<html>
<head>
<title>Simple HTML Photo Gallery with JavaScript</title>

<style type="text/css">
body {
	background: #222;
	color: #eee;
	margin-top: 20px;
	font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
}
a {
	color: #FFF;
}
a:hover {
	color: yellow;
	text-decoration: underline;
}
.thumbnails img {
	height: 80px;
	border: 4px solid #555;
	padding: 1px;
	margin: 0 10px 10px 0;
}

.thumbnails img:hover {
	border: 4px solid #00ccff;
	cursor:pointer;
}

.preview img {
	border: 4px solid #444;
	padding: 1px;
	width: 900px;
}
</style>

</head>
<body>

<div class="gallery" align="center">
	<br />

	<div class="thumbnails">
		<img onmouseover="preview.src=img1.src" name="img1" src="/resources/images/seabeach.jpg" alt=""/>
		<img onmouseover="preview.src=img2.src" name="img2" src="/resources/images/seabridge.jpg" alt=""/>
		<img onmouseover="preview.src=img3.src" name="img3" src="/resources/images/searock.jpg" alt=""/>
		<img onmouseover="preview.src=img4.src" name="img4" src="/resources/images/seaside.jpg" alt=""/>
	</div><br/>

	<div class="preview" align="center">
		<img name="preview" src="/resources/images/seabeach.jpg" alt=""/>
	</div>

</div>

</body>
</html>