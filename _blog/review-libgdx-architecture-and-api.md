---
title: "Review: LibGDX Architecture and API "
excerpt: "<img style='margin-top:10px;' src='/images/libgdx.png'>"
collection: blog
---

<center><img style="margin-top:2%; margin-bottom:2%" src='/images/libgdx.png'></center>

<div id="app_framework">
	<h1 style="color:blue;">The Application Framework</h1>
	<p align="justify">
		Libgdx terdiri dari enam interface yang menyediakan sarana untuk berinteraksi dengan sistem operasi. Setiap back-end mengimplementasikan antarmuka ini, diantara lain Application, Files, Input, Net, Audio, dan Graphics. 
	</p>

	<h2>The Life Cycle</h2>
		<center><img src='/images/lifecycle.png'></center>

	<h2>Modules Oveview</h2>
		<p align="justify">
			LibGDX terdiri dari beberapa modul yang menyediakan layanan untuk setiap langkah arsitektur permainan yang khas. Sebagai berikut : Input, Graphic, File, Audio, dan Networking.
		</p>

		<center><img src='/images/modules.png'></center>

	<h2>Querying</h2>
		<p align="justify">The Application interface provides various methods to query properties of the run-time environment.</p>
	
	<h2>Logging</h2>
		<p align="justify">Tergantung pada platformnya. Misalnya Console (Desktop), LogCat (Android) atau GWT TextArea yang disediakan di GwtApplicationConfiguration atau dibuat secara otomatis (html5)</p>

	<h2>Threading</h2>
		<p align="justify">
			Semua metode ApplicationListener dipanggil pada thread yang sama. Thread ini adalah thread rendering dimana panggilan OpenGL dapat dilakukan. Untuk kebanyakan game, cukup untuk menerapkan pembaruan logika dan rendering dalam metode ApplicationListener.render (), dan pada thread rendering.
		</p>
		<p align="justify">
			Setiap operasi grafis yang secara langsung melibatkan OpenGL perlu dijalankan pada thread rendering. Untuk melewatkan data ke thread rendering dari thread lain, disarankan untuk menggunakan Application.postRunnable (). Ini akan menjalankan kode di Runnable di thread rendering di frame berikutnya, sebelum ApplicationListener.render () dipanggil.
		</p>

</div>

<div id="file_handling">
	<h1 style="color:blue;">File Handling</h1>
	<p align="justify">
		Aplikasi Libgdx berjalan di empat platform yang berbeda: Desktop (Windows, Linux, Mac OS X, Headless), Android, iOS, dan JavaScript / WebGL. Code di LibGDX biasanya digunakan untuk Membaca File (read), Menulis file (write), menyalin file (copy), memindahkan file (move), menghapus file (delete), mendaftarkan file dan menaruh di directory, dan memeriksa file. 
	</p>
	<p align="justify">
		File Storage dibagi 5 antara lain :
		<ul>
			<li>Classpath</li>
			<li>Internal </li>
			<li>Local </li>
			<li>External </li>
			<li>Absolute </li>
		</ul>

	</p>
	<p align="justify">
		File Handling juga bisa mengecek tersedianya penyimpanan dan jalurnya, mendapatkan FileHandler, mendaftarkan dan mengecek properti dari file.
	</p>
</div>

<div id="networking">
	<h1 style="color:blue;">Networking</h1>
	<p align="justify">
		LibGDX mencakup beberapa kelas untuk operasi jaringan lintas platform. Kelas-kelas ini lebih dikenal sebagai Gdx.net.<br>
		Fitur :
		<ul>
			<li>Permintaan HTTP lintas platform</li>
			<li>Dukungan multi-platform TCP client dan server socket (tidak termasuk GWT) dengan pengaturan yang dapat dikonfigurasi</li>
			<li>Pengaturan klien dan server TCP yang optimal yang bertujuan untuk low-latency</li>
			<li>Akses browser lintas platform</li>
		</ul>

		<br><br>
		Implementasinya
		<ul>
			<li>NET.java</li>
			<li>Socket.java </li>
			<li>SocketHints.java </li>
			<li>ServerSocket.java </li> 
			<li>ServerSocketHints.java</li>
			<li>HttpStatus.java</li>
			<li>HttpParameterUtils.java</li>
			<li>HttpRequestBuilder</li>
		</ul>
	</p>
</div>

<div id="preferences">
	<h1 style="color:blue;">Preferences</h1>
	<p align="justify">
		Preferensi adalah cara sederhana untuk menyimpan data kecil untuk sebuah aplikasi. Preferensi bekerja seperti peta hash, menggunakan string sebagai kunci, dan berbagai tipe primitif sebagai nilai. <br>
		Preferensi diperoleh melalui codingan berikut ini:
	</p>
	<p style="margin-left: 5%">Preferences prefs = Gdx.app.getPreferences("My Preferences");</p>
	<p align="justify">
		<b>Read and Write Value</b>
		Berikut cara memodifikasi Preferensi :
		<p style="margin-left: 5%">
			prefs.putString("name", "Donald Duck");<br>String name = prefs.getString("name", "No name stored");<br>prefs.putBoolean("soundOn", true);<br>prefs.putInteger("highscore", 10);
		</p> 
	</p>

	<p align="justify">
		<b>Flushing</b>
		Perubahan yang dilakukan ke instance preferensi hanya akan bertahan jika Anda secara eksplisit memanggil metode flush().
	</p>

	<p align="justify">
		<b>Storage</b>
		Pada Windows, Linux, dan OS X, preferensi disimpan dalam file xml di dalam direktori home pengguna.<br>
		Windows : %UserProfile%/.prefs/My Preferences<br>
		Linux dan OS X : ~/.prefs/My Preferences
	</p>
</div>

<div id="input_handling">
	<h1 style="color:blue;">Input Handling</h1>
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
					kemudian mengecek ketersediaannya pada perangkat menggunakan method Gdx.input.isPeripheralAvailable(Peripheral. Gyroscope);
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
	<h1 style="color:blue;">Memory Management</h1>
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
	<h1 style="color:blue;">Audio</h1>
	<p align="justify">
		Libgdx menyediakan metode untuk memutar ulang efek suara kecil serta mengalirkan potongan musik yang lebih besar langsung dari disk.
		<p style="margin-left: 5%">Audio audio = Gdx.audio;</p>
	</p>

	<p align="justify">
		Bagian-bagian Audio antara lain:
		<ul>
			<li>Sound Effect</li>
				<p align="justify">
					Sound Effect adalah sampel audio kecil, biasanya tidak lebih dari beberapa detik. Efek suara bisa disimpan dalam berbagai format. Libgdx mendukung file MP3, OGG dan WAV. RoboVM (iOS) saat ini tidak mendukung file OGG.
				</p>
			<li>Streaming Music</li>
				<p align="justify">
					Untuk memuat contoh Musik kita dapat melakukan hal berikut:
					<p style="margin-left: 5%">
						Music music = Gdx.audio.newMusic(Gdx.files.internal("data/mymusic.mp3"));
					</p>
				</p>
			<li>Playing PCM Audio</li>
				<p align="justify">
					Modul audio dapat memberi Anda akses langsung ke perangkat keras audio untuk menulis sampel PCM ke dalamnya.<br>

					Untuk membuat instance AudioDevice baru, antara lain sebagai berikut:
					<p style="margin-left: 5%">AudioDevice device = Gdx.audio.newAudioDevice(44100, true);</p>

					Kita bisa menulis data PCM yang dilepaskan 16 bit atau data PCM 32-bit float ke perangkat:
					<p style="margin-left: 5%">
						float[] floatPCM = ... generated from a sine for example ...<br>device.writeSamples(floatPCM, 0, floatPCM.length);<br><br>short[] shortPCM = ... generated from a decoder ...<br>device.writeSamples(shortPCM, 0, shortPCM.length);
					</p>

				</p>
			<li>Recording PCM Audio</li>
				<p align="justify">
					Anda dapat mengakses data PCM dari mikrofon pada PC atau ponsel Android melalui antarmuka AudioRecorder .
					<p style="margin-left: 5%"> AudioRecorder recorder = Gdx.audio.newAudioRecorder(22050, true);</p>
				</p>
		</ul>

	</p>

</div>

<div id="graphics">
	<h1 style="color:blue;">Graphics</h1>
	<p></p>
</div>

<div id="managing_asset">
	<h1 style="color:blue;">Managing Your Assets</h1>
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
	<h1 style="color:blue;">Internationalization and Localization</h1>
	<p align="justify">
		Internationalization adalah proses perancangan perangkat lunak sehingga bisa berpotensi disesuaikan dengan berbagai bahasa tanpa perubahan teknik. Localization adalah proses mengadaptasinya perangkat lunak internationalization dengan menambah komponen lokal. Internationalization dan Localization sering disingkat menjadi i18n dan l10n. 
	</p>
	<p align="justify">
		Di LibGdx class I18NBundle digunakan untuk store dan fetch strings yang local sensitive. Bundle memungkinkan untuk mempermudah menterjemahkan pada perangkat lunak.
	</p>
</div>

<div id="utilities">
	<h1 style="color:blue;">Utilities</h1>
	<h2>Reading and Writing JSON</h2>
		<p align="justify">
			Beberapa Perintah yang ada di libgdx untuk menggunakan fungsi JSON
			<ol>
			<li>JsonWriter: membuat style API untuk mengeluarkan dengan menggunakan JSON. </li>
			<li>JsonReader: parsing JSON dan membangun sebuah DOM dengan objek dari JsonValue</li>
			<li>JsonValue: Berupa sebuah JsonObject,array,string,float,long,Boolean,atau null.</li>
			<li>Json: menulis atau membaca semaunya object graph dengan menggunakan JsonReader & JsonWriter</li>
			</ol>
		</p>

	<h2>Reading and Writing XML</h2>
		<p align="justify">
			Sama seperti JSON XML mempunyai 2 fungsi yaitu XMLReader(code) untuk membaca file yang bertype XML ke sebuah DOM . dan XMLWriter(code) digunakan untuk menggunakan API dan mengeluarkan data XML.
		</p>
	<h2>Collections</h2>
		<ol>
			<li>List</li>
			<li>Primitive List</li>
				<p>
					<ul>
						<li>IntAray()</li>
						<li>FloatArray()</li>
						<li>BooleanArray()</li>
						<li>CharArray()</li>
						<li>LongArray()</li>
						<li>ByteArray()</li>
					</ul>
				</p>
			<li>Specialized Array</li>
				<p>
					<ul>
						<li>SnapshotArray()</li>
						<li>DelayedRemovalArray()</li>
						<li>PooledLinkedList()</li>
						<li>SortedIntList()</li>
					</ul>
				</p>
			<li>Maps</li>
				<p>
					<ul>
						<li>Primitive Maps : IntMap(), LongMap(), ObjectInMap(), ObjectFloatMap() </li>
						<li>Specialized Maps : OrderedMap(), IdentityMap(), ArrayMap()</li>
					</ul>
				</p>
			<li>Sets</li>
			<li>BinaryHeap</li>
				<p>
					Bisa berupa min-heap atau max-heap
				</p>
		</ol>
	<h2>Reflection</h2>
		<p align="justify">
			Untuk memanfaatkan refleksi dengan cara cross-platform, LibGDX menyediakan bungkus kecil di sekitar Java’s Reflection API. Pembungkus terdiri dari dua kelas yang berisi metode statis yang akan Anda gunakan untuk melakukan operasi refleksi: <br>

			ArrayReflection = fungsi array yg diambil dari API java.lang.reflect.array<br>
			ClassReflection = fungsi class yg diambil dari java.lang.class

		</p>
	<h2>Jnigen</h2>
		<p align="justify">
			Jnigen adalah perpustakaan kecil yang bisa digunakan dengan atau tanpa libgdx yang memungkinkan kode C / C ++ untuk ditulis sejajar dengan kode sumber Java. Hal ini meningkatkan lokalitas kode yang dimiliki bersama secara konseptual (metode kelas asli Jawa dan penerapan sebenarnya) dan membuat refactoring jauh lebih mudah dibandingkan dengan alur kerja JNI biasa.
		</p>
		<p align="justify">
			<b>GWT<b><br>
			Untuk menggunakan fungsi GWT ini tidak sama dengan cara menggunakan reflection pada umumnya. Jika ingin menggunakan GWT dan mengimplementasikan refleksi maka harus mengdeclare class mana yang ingin di refleksi. Saat mengkompilasi proyek HTML, LibGDX mengambil informasi itu dan menghasilkan cache refleksi yang berisi informasi tentang dan menyediakan akses ke konstruktor, bidang, dan metode kelas yang ditentukan. LibGDX kemudian menggunakan cache refleksi ini untuk mengimplementasikan refleksi api.
		</p>

</div>

<div id="math_utilities">
	<h1 style="color:blue;">Math Utilities</h1>
	<p align="justify">
		MathUtils (kode) mencakup sejumlah peluang dan tujuan yang berguna. Ada anggota Random Statis yang praktis untuk menghindari instantiating satu kode Anda sendiri. Menggunakan contoh acak yang sama di seluruh kode Anda juga dapat memastikan perilaku deterministik secara konsisten asalkan Anda menyimpan nilai benih yang digunakan. Ada konstanta untuk konversi antara radian dan derajat serta tabel look-up untuk fungsi sinus dan kosinus. Ada juga versi float fungsi java.lang.Math umum untuk menghindari harus dilemparkan dari ganda.
	</p>

	<p align="justify">
		<h2>Interpolasi</h2>
		Umumnya dikenal sebagai tweening, interpolasi berguna untuk menghasilkan nilai antara dua titik akhir diskrit dengan menggunakan berbagai fungsi kurva. Sering digunakan dengan animasi berbingkai kunci, interpolasi memungkinkan seorang animator untuk menentukan kumpulan frame eksplisit yang jarang untuk animasi dan kemudian menghasilkan transisi yang mulus antara kerangka ini secara komputasi.
		Type of Interpolation : Bounce, Circle, Elastic, Exponential, Fade, Power, Sine, dan Swing.
	</p>

	<p align="justify">
		<h2>Vector , Matric, dan Quaternions</h2>
		<ul>
			<li>Vector</li>
			<p align="justify">
				Vektor adalah deretan angka yang digunakan untuk menggambarkan sebuah konsep dengan arah dan besaran seperti posisi, kecepatan, atau percepatan
			</p>
			<li>Matric</li>
			<p align="justify">
				Matriks adalah deret angka dua dimensi. Matriks digunakan dalam grafik untuk melakukan transformasi dan proyeksi verteks di ruang 3D untuk display pada layar 2D. Seperti OpenGL, Libgdx menyimpan matriks dalam urutan kolom utama. Matriks datang dalam varietas 3x3 (Matrix3) (kode) dan 4x4 (Matriks4) (kode) dengan metode yang mudah digunakan untuk memindahkan nilai di antara keduanya. Libgdx mencakup banyak operasi umum untuk bekerja dengan matriks seperti transformasi penerjemahan dan penskalaan, rotasi bangunan dari sudut Euler, pasang sudut sumbu atau kuota, proyeksi bangunan, dan perbanyakan dengan matriks dan vektor lainnya.
			</p>
			<li>Quaternions</li>
			<p align="justify">
				Quaternions adalah sistem bilangan empat dimensi yang memperpanjang bilangan kompleks. Mereka memiliki banyak kegunaan esoteris dalam teori matematika dan bilangan yang lebih tinggi. Khususnya dalam konteks Libgdx penggunaan unit-quaternions dapat berguna untuk menggambarkan rotasi dalam ruang tiga dimensi, karena memberikan komposisi yang lebih sederhana, stabilitas numerik, dan penghindaran kunci gimbal sehingga lebih sering disukai pada metode representasi rotasi lainnya. mungkin banyak jatuh pendek di daerah ini.
			</p>
		</ul>
	</p>

	<p align="justify">
		<h2>Circle, Planes, etc.</h2>
		<ul>
			<li>Bounding Boxes</li>
			<p align="justify">
				Kotak pembatas sumbu-selaras yang berguna untuk uji persimpangan volume sederhana. Ini ditentukan oleh titik minimum dan maksimum yang menjelaskan luasan persegi panjang volumenya.
			</p>
			<li>Circle</li>
			<p align="justify">
				Kelas sederhana yang menggambarkan sebuah lingkaran dengan titik tengah dan jari-jari.
			</p>
			<li>Frustum</li>
			<p align="justify">
				Sebuah frustum adalah piramida empat sisi dengan potongan paling atas. Hal ini dapat digunakan untuk menggambarkan volume yang terlihat pada tampilan segi empat ke dalam ruang dengan proyeksi perspektif seperti halnya adegan 3D yang diproyeksikan ke monitor 2D.
			</p>
			<li>Planes</li>
			<p align="justify">
				Plane adalah permukaan dua dimensi tak terbatas di ruang tiga dimensi yang digambarkan oleh sebuah titik di permukaan itu dan permukaan yang normal. Pesawat dapat berguna untuk mempartisi ruang dan menentukan sektor mana yang berada pada suatu objek. Persimpangan dengan sinar (kode) atau segmen garis dapat diuji untuk menggunakan kelas Intersektor (kode).
			</p>
			<li>Polygons</li>
			<p align="justify">
				Sebuah kelas sederhana yang mendefinisikan poligon dua dimensi dari daftar titik. Hal ini dapat dengan mudah diterjemahkan, diputar, dan diskalakan. Ini juga menyediakan kemampuan untuk menguji titik untuk penahanan di dalam poligon. Perpotongan poligon ke poligon dapat diuji dengan menggunakan kelas Intersektor (kode), dengan asumsi poligon bersifat cembung.
			</p>
			<li>Rays</li>
			<p align="justify">
				Rays adalah segmen garis tak terbatas dalam satu arah. Ini ditentukan oleh asal dan arah satuan-panjang
			</p>
			<li>Rectangle</li>
			<p align="justify">
				Sebuah kelas sederhana yang menggambarkan persegi panjang sumbu-selektif dua dimensi yang digambarkan oleh titik sudut kiri bawah dan lebar dan tinggi.
			</p>
			<li>Segment</li>
			<p align="justify">
				Sebuah kelas sederhana yang menggambarkan segmen garis dalam ruang tiga dimensi yang didefinisikan oleh dua titik akhir.
			</p>
			<li>Spheres</li>
			<p align="justify">
				Kelas sederhana yang menggambarkan bidang tiga dimensi yang didefinisikan oleh titik pusat dan radius.
			</p>
		</ul>
	</p>

	<p align="justify">
		<h2>Path Interface and Splines</h2>
		<p align="justify">
			Path Interface (code) memiliki implementasi yang memungkinkan Anda melintasi dengan lancar melalui serangkaian titik pasti (dalam beberapa kasus, garis singgung juga). Jalur dapat didefinisikan sebagai dimensi dua atau tiga dimensi, karena ini adalah templat yang mengambil turunan kelas Vektor, sehingga Anda dapat menggunakannya dengan seperangkat Vector2 atau Vector3's.
		</p>
		
	</p>
</div>

<div id="tools">
	<h1 style="color:blue;">Tools</h1>
	<p></p>
</div>

<div id="extentions">
	<h1 style="color:blue;">Extentions</h1>
	<p></p>
</div>

<div id="third_party">
	<h1 style="color:blue;">Third Party Services</h1>
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