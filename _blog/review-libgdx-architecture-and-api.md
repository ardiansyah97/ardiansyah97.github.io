---
title: "Review: LibGDX Architecture and API "
excerpt: "<img style='margin-top:10px;' src='/images/libgdx.png'>"
collection: blog
---

<center><img style="margin-top:2%; margin-bottom:2%" src='/images/libgdx.png'></center>

<div id="app_framework">
	<h1>The Application Framework</h1>
	<p></p>
</div>

<div id="file_handling">
	<h1>File Handling</h1>
	<p></p>
</div>

<div id="networking">
	<h1>Networking</h1>
	<p></p>
</div>

<div id="preferences">
	<h1>Preferences</h1>
	<p></p>
</div>

<div id="input_handling">
	<h1>Input Handling</h1>
	<div>
			<p align="justify">
				Setiap platform memiliki input yang berbeda. Pada desktop input dapat berupa mouse dan keyboard. Hal yang sama juga berlaku untuk game browser. Di Android, mouse digantikan dengan touch screen. Android juga dapat mendapatkan input dari sensor yang ada di perangkatnya. Sekarang ini perangkat Android telah dilengkapi dengan berbagai sensor, seperti accelerometer, gyroscope, dan magnetic field sensor. </p>

			<h2>Configuration and Querying</h2>
			<p align="justify">
				Pada LibGdx untuk mengaktifkan dan menon-aktifkan perangkat input dapat dikonfigurasi menggunakan class AndroidApplicationConfiguration.
				<p style="margin-left: 5%">
					AndroidApplicationConfiguration config = new AndroidApplicationConfiguration(); <br>config.useAccelerometer = false; <br>config.useCompass = false;<br>config.useGyroscope = true;<br>initialize(new MyGame(), config);
				</p>

				Sedangkan untuk mengetahui input yang tersedia pada platform saat game dijalankan dapat menggunakan method Input.isPeripheralAvailable();
				<p style="margin-left: 5%; margin-top: 2%">
					boolean multiTouch = Gdx.input.isPeripheralAvailable(Peripheral.MultitouchScreen);</p> 
				</p>
			
			<h2>Mouse, Touch, and Keyboard</h2>
				<p align="justify">
					Input utama yang disupport libgdx yaitu mouse untuk desktop/browser, touch screen di Android, dan keyboard.
				</p>
				<h3>Keyboard</h3>
					<p>Tiga method utama untuk mendengarkan keyboard events :</p>
					<ol>
						<li>keyDown() : dipanggil ketika tombol ditekan.</li>
						<li>keyUp() : dipanggil ketika tombol dilepas.</li>
						<li>keyTyped() : dipanggil ketika karakter Unicode degenerate oleh input keyboard.</li>
					</ol>

				<h3>Mouse and Touch</h3>
					<p>Lima method untuk mendengarkan mouse & touch events :</p>
					<ol>
						<li>touchDown() : dipanggil ketika mouse di tekan atau layer di sentuh.</li>
						<li>touchUp() : dipanggil ketika mouse atau sentuhan di lepas.</li>
						<li>touchDragged() :  dipanggil ketika mouse atau touch di drag.</li>
						<li>mouseMoved() : dipanggil ketika mouse berpindah posisi pada layar tanpa menekan tombol pada mouse.</li>
						<li>scrolled() : dipanggil ketika scroll pada mouse diputar.</li>
					</ol>

			<h2>Controller</h2>
				<p align="justify">
					Class Controller memiliki method untuk memeriksa perangkat keras yang terhubung, yaitu Controllers.getControllers().
				</p>

				<p align="justify">
					Controller mempunyai beberapa komponen:
					<ul>
						<li>Button</li>
						<li>Axes</li>
						<li>POVs</li>
						<li>Slider and Accelerometer</li>
					</ul>
				</p>

				<p align="justify">
					Polling untuk keadaan tertentu dapat dilakukan seperti berikut:
					<p style="margin-left: 5%">
						boolean buttonPressed = controller.getButton(buttonCode);<br>float axisValue = controller.getAxis(axisCode);
					</p>
				</p>

				<p align="justify">
					LibGdx menyediakan register listener untuk menerima controller events. Interface yang di implementasi untuk mendengarkan controller event disebut ControllerListener.
				</p>

			<h2>Gesture Detection</h2>
				<p align="justify">
					LibGdx menyediakan GestureDetector yang memungkinkan untuk mendeteksi gesture:
					<ol>
						<li><b>touchDown</b> : pengguna menyentuh layar</li>
						<li><b>longPress</b> : pengguna menyentuh layar untuk beberapa waktu</li>
						<li><b>tap</b> : pengguna menyentuh layar kemudian melepas dan menyentuh kembali layar pada area yang sama. Detector akan melaporkan koordinat saat ini dan delta antara posisi awal dan akhir</li>
						<li><b>pan</b> : pengguna men-drag (menyeret) jari di layar</li>
						<li><b>panStop</b> : dipanggil ketika tidak lagi panning</li>
						<li><b>fling</b> : pengguna menyeret jari di layar, kemudian mengangkatnya. Berguna untuk mengimplementasi swipe gesture</li>
						<li><b>zoom</b> : pengguna menempatkan dua jari di layar kemudian memindahkannya (menyeretnya) secara bersama-sama</li>
						<li><b>pinch : mirip dengan zoom</b></li>
					</ol>
				</p>

				<p align="justify">
					Untuk me-listen gesture harus mengimplement GestureListener interface dan mengirimnya ke konstruktor GestureDetector.
				</p>

			<h2>Simple Text Input</h2>
				<p align="justify">
					Untuk menerima input atau notifikasi ketika input dibatalkan, yang harus di implement adalah TextInputListener interface.
				</p>

			<h2>Accelerometer</h2>
				<p align="justify">
					Untuk menggunakan accelerometer, yang pertama kali harus dilakukan yaitu mengecek ketersediaannya ada perangkat menggunakan method Gdx.input.isPeripheralAvailable(Peripheral.Accelerometer);
				</p>
				<p align="justify">
					Jika game membutuhkan orientasi, dapat didapatkan menggunakan method Gdx.input.getRotation(); atau Gdx.input.getNativeOrientation();
				</p>
				<p align="justify">
					Untuk membaca accelerometer dengan LibGdx menggunakan method 
					<p style="margin-left: 5%">
						<ul>
							<li>float accelX = Gdx.input.getAccelerometerX();</li>
							<li>float accelY = Gdx.input.getAccelerometerY();</li>
							<li>float accelZ = Gdx.input.getAccelerometerZ();</li>
						</ul>
					</p>
				</p>

			<h2>Compass</h2>
				<p align="justify">
					Untuk menggunakan compass, yang pertama kali harus dilakukan yaitu mengecek ketersediaannya ada perangkat menggunakan method Gdx.input.isPeripheralAvailable(Peripheral.Compass);
				</p>
				<p align="justify">
					Dan untuk mendapatkan sumbu x, y, dan z dapat menggunakan polling berikut:
					<ul>
						<li>float azimuth = Gdx.input.getAzimuth(); //sumbu z</li>
						<li>float pitch = Gdx.input.getPitch(); //sumbu x</li>
						<li>float roll = Gdx.input.getRoll(); //sumbu y</li>
					</ul>
				</p>

			<h2>Gyroscope</h2>
				<p align="justify">
					Untuk menggunakan gyroscope, yang pertama kali harus dilakukan yaitu mengaktifkan gyroscope pada perangkat Android dengan 
					<p style="margin-left: 5%">
						AndroidApplicationConfiguration  config = new AndroidApplicationConfiguration();<br>config.useGyroscope = true;
					</p>
					kemudian mengecek ketersediaannya ada perangkat menggunakan method Gdx.input.isPeripheralAvailable(Peripheral. Gyroscope);
				</p>

				<p>
					Untuk mendapatkan sumbu x, y, dan z dapat menggunakan polling berikut:
					<ul>
						<li>float gyroX = Gdx.input.getGyroscopeX();</li>
						<li>float gyroY = Gdx.input.getGyroscopeY();</li>
						<li>float gyroZ = Gdx.input.getGyroscopeZ();</li>
					</ul>
				</p>

			<h2>Vibrator</h2>
				<p align="justify">
					Vibrator hanya tersedia pada perangkat Android, dan membutuhkan permission pada file manifest untuk menggunakannya.
					<p style="margin-left: 5%">
						android.permission.VIBRATE
					</p>
				</p>

			<h2>Cursor Visibility & Catching</h2>
				<p align="justify">
					Cursor catching dan positioning hanya tersedia pada desktop. Dan ketika cursor tidak dibutuhkan lagi, cursor tersebut seharusnya dibuang (dispose)
				</p>

			<h2>Back & Menu Key Catching</h2>
				<p align="justify">
					Untuk menggunakan tombol back & menu pada perangkat Android, yang harus dilakukan yaitu dengan melakukan method berikut:
					<p style="margin-left: 5%">
							Gdx.input.setCatchBackKey(true); // tombol back<br>Gdx.input.setCatchMenuKey(true); // tombol menu
					</p>
				</p>

			<h2>On-Screen Keyboard</h2>
				<p align="justify">
					Untuk memunculkan on-screen keyboard pada Android perlu menggunakan method
					<p style="margin-left: 5%">
						Gdx.input.setOnscreenKeyboardVisible(true);
					</p>
				</p>
	</div>

</div>

<div id="memory_management">
	<h1>Memory Management</h1>
	<p align="justify">
		Libgdx mempunyai beberapa class yang menerapkan antarmuka sekali pakai yang mengindikasikan bahwa id ini harus dibuang secara manual pada akhir masa pakai. Kegagalan membuang (dispose) sumber daya akan menyebabkan kebocoran memori yang parah!
	</p>
	<p align="justify">Berikut ini merupakan class yang membutuhkan untuk dibuang secara manual.
		<ul>
			<li>AssetManager</li>
			<li>Bitmap</li>
			<li>BitmapFont</li>
			<li>BitmapFontCache</li>
			<li>CameraGroupStrategy</li>
			<li>DecalBatch</li>
			<li>ETC1Data</li>
			<li>FrameBuffer</li>
			<li>Mesh</li>
			<li>Model</li>
			<li>ModelBatch</li>
			<li>ParticleEffect</li>
			<li>Pixmap</li>
			<li>PixmapPacker</li>
			<li>Shader</li>
			<li>ShaderProgram</li>
			<li>Shape</li>
			<li>Skin</li>
			<li>SpriteBatch</li>
			<li>SpriteCache</li>
			<li>Stage</li>
			<li>Texture</li>
			<li>TextureAtlas</li>
			<li>TileAtlas</li>
			<li>TileMapRenderer</li>
			<li>com.badlogic.gdx.physics.box2d.World</li>
			<li>all bullet classes</li>
		</ul>
	</p>

	<p align="justify">
		<h3>Object Pooling</h3>
		Prinsip object pooling adalah penggunaan kembali objek yang tidak aktif atau mati, alih-alih menciptakan objek baru setiap saat. LibGdx menawarkan beberapa tools untuk penggabungan yang mudah:
		<ul>
			<li>Poolable Interface</li>
				<p align="justify">
					Objek yang mengimplementasikan interface ini akan memiliki reset () yang dipanggil saat dilewatkan ke Pool.free (Object).
				</p>
			<li>Pool</li>
				<p align="justify">
					Kolam objek yang bisa digunakan kembali untuk menghindari alokasi.
				</p>
			<li>Pools</li>
				<p align="justify">
					Menyimpan peta Pools (biasanya ReflectionPools) menurut jenis untuk akses statis yang mudah digunakan.
				</p>
		</ul>
	</p>
</div>

<div id="audio">
	<h1>Audio</h1>
	<p></p>
</div>

<div id="graphics">
	<h1>Graphics</h1>
	<p></p>
</div>

<div id="managing_asset">
	<h1>Managing Your Assets</h1>
	<p align="justify">
		AssetManager membantu untuk memuat dan mengelola asset. Berikut cara yang disarankan untuk memuat asset:
		<ul>
			<li>Pemuatan resource dilakukan secara asinkron</li>
			<li>Menyiman semua asset pada satu tempat</li>
			<li>Memungkinkan transparently implement seperti cache </li>
		</ul>
	</p>

	<p align="justify">
		Untuk membuat AssetManager menggunakan code seperti berikut
		<p style="margin-left: 5%">AssetManager manager = new AssetManager();</p>
		Kemudian untuk meload asset menggunakan fungsi load()
		<p style="margin-left: 5%">manager.load("data/mytexture.png", Texture.class);</p>
	</p>
	<p align="justify">
		Jika asset masih dalam proses loading, maka kita wajib memanggil fungsi AssetManager.update(). Jika proses loading telah selesai, pangil manager.finishLoading();
	</p>
	<p align="justify">
		Untuk mendapatkan asset dapat menggunakan fungsi get(); 
		<p style="margin-left:5%">Texture tex = manager.get("data/mytexture.png", Texture.class);</p>
	</p>
	<p align="justify">
		Apabila asset tidak terpakai lagi, dapat dibuang menggunakan fungsi unload()
		<p style="margin-left: 5%">manager.unload("data/myfont.fnt");</p>
		Jika ingin menghapus semua asset sekali panggil, gunakan fungsi clear() atau dispose()

		<p style="margin-left: 5%">manager.clear();</p>
		<p style="margin-left: 5%">manager.dispose();</p>
	</p>
</div>

<div id="inter_local">
	<p></p>
</div>

<div id="utilities">
	<h1>Utilities</h1>
	<p></p>
</div>

<div id="math_utilities">
	<h1>Math Utilities</h1>
	<p></p>
</div>

<div id="tools">
	<h1>Tools</h1>
	<p></p>
</div>

<div id="extentions">
	<h1>Extentions</h1>
	<p></p>
</div>

<div id="third_party">
	<h1>Third Party Services</h1>
	<p>Libgdx bisa diintegrasikan dengan banyak third party services, seperti :
	<ul>
		<li>Admob</li>
		<li>Google Mobile Ads</li>
			<p align="justify">
				Me-replace Admob yang deprecated. Google AdMob adalah layanan iklan nomor satu yang  digunakan developer Android dan LibGdx
			</p>
		<li>Swarm</li>
		<li>NextPeer</li>
		<li>Google Play Game Services</li>
			<p align="justify">
				Menawarkan platform dengan leaderboard, achievement, dan banyak lagi (realtime multiplayer, cloud save, anti-piracy)
			</p>
	</ul>

	</p>
</div>