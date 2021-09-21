<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="bootstrap.min.css">
	<title>Text shadow Generator Z@K</title>
	<style>
		body {
			text-align: center;
			background-color: #eeeeee;
		}

		label {
			display: block;
		}

		h1 {
			text-transform: uppercase;
			font-weight: bold;
			letter-spacing: 6px;
			font-size: 40px;
			color: #000000;
			margin-top: 15px;
			margin-bottom: 15px;
		}

		input[type="range"] {
			width: 100%;
		}

		input[type="color"] {
			border: none;
			background-color: transparent;
			width: 55px;
			height: 55px;
			padding: 0;
			margin-bottom: 15px;
		}

		input[type="color"]:hover {
			cursor: pointer;
		}

		textarea {
			width: 100%;
			resize: none;
			margin-bottom: 15px;
			max-width: 300px;
			font-size: 13px;
		}

		.card {
			height: 100%;
		}

		.card-header {
			font-weight: bold;
			color: #ffffff;
		}

		.row>div {
			margin-bottom: 15px;
		}
	</style>
</head>

<body>
	<h1>Text shadow</h1>
	<div class="container">
		<div class="row">
			<div class="col-xl-4 col-md-6">
				<div class="card">
					<div class="card-header bg-primary">Настройки</div>
					<div class="card-body">
						<label for="font_size">Размер шрифта</label>
						<input class="custom-range" id="font_size" type="range" min="8" max="40" step="1" value="40">
						<label for="offset_x">Смещение по оси x</label>
						<input class="custom-range" id="offset_x" type="range" min="-15" max="15" step="1" value="4">
						<label for="offset_y">Смещение по оси y</label>
						<input class="custom-range" id="offset_y" type="range" min="-15" max="15" step="1" value="-1">
						<label for="blur">Размытие</label>
						<input class="custom-range" id="blur" type="range" min="0" max="15" step="1" value="0">
					</div>
				</div>
			</div>
			<div class="col-xl-4 col-md-6">
				<div class="card">
					<div class="card-header bg-primary">Цвет</div>
					<div class="card-body">
						<input type="color" value="#ff0000">
						<label for="opacity">Прозрачность</label>
						<input class="custom-range" id="opacity" type="range" min="0" max="1" step="0.01" value="1">
					</div>
				</div>
			</div>
			<div class="col-xl-4 col-md-12">
				<div class="card">
					<div class="card-header bg-primary">Результат</div>
					<div class="card-body">
						<label for="resultHex">Цвет в HEX</label>
						<textarea id="resultHex" rows="4" readonly></textarea><br>
						<label for="resultRgba">Цвет в RGBA</label>
						<textarea id="resultRgba" rows="3" readonly></textarea><br>
					</div>
				</div>
			</div>
		</div>
	</div>
	<script src="jquery-3.6.0.min.js"></script>
	<script>
		function cssShadow({
			font_size,
			offset_x,
			offset_y,
			blur,
			opacity,
			color,
			rgba
		}) {
			var cssStyles = offset_x + 'px' + offset_y + 'px' + blur + 'px' + rgba;
			$('h1').css('text-shadow', cssStyles);
			$('#resultHex').val('background-color:' + color + ';\nopacity: ' + opacity + '\nfont-size: ' + font_size + 'px;');
			$('#resultRgba').val('text-shadow:' + offset_x + 'px ' + offset_y + 'px ' + blur + 'px ' + rgba + ';\nfont-size: ' + font_size + 'px;');

		}
		cssShadow({
			font_size: 40,
			offset_x: 4,
			offset_y: -1,
			blur: 0,
			opacity: 1,
			color: '#ff0000',
			rgba: 'rgba(255, 0, 0, 1)'
		});
		$(document).on('input change', 'input', function () {
			var font_size = $('#font_size').val();
			var offset_x = $('#offset_x').val();
			var offset_y = $('#offset_y').val();
			var blur = $('#blur').val();
			var opacity = $('#opacity').val();
			var color = $('input[type="color"]').val() + '';
			var red16 = color[1] + '' + color[2];
			var green16 = color[3] + '' + color[4];
			var blue16 = color[5] + '' + color[6];
			var red10 = parseInt(red16, 16);
			var green10 = parseInt(green16, 16);
			var blue10 = parseInt(blue16, 16);
			var rgba = 'rgba(' + red10 + ', ' + green10 + ', ' + blue10 + ', ' + opacity + ')';

			$('h1').css('fontSize', font_size + 'px');
			cssShadow({
				font_size: font_size,
				offset_x: offset_x,
				offset_y: offset_y,
				blur: blur,
				opacity: opacity,
				color: color,
				rgba: rgba
			});
		})
	</script>
</body>

</html>
