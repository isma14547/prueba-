<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teknovae - Tu Tienda de Tecnología</title>
    <!-- Incluir Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Configuración de la fuente Inter para todo el cuerpo -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Estilos personalizados para el scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #555;
        }

        /* Estilo para el banner principal con imagen de fondo */
        .hero-banner {
            background-size: cover;
            background-position: center;
            height: 70vh; /* Altura del banner */
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            color: white;
            position: relative;
            overflow: hidden;
        }

        .hero-banner::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.55); /* Oscurece la imagen para que el texto sea legible */
            z-index: 0;
        }

        .hero-content {
            position: relative;
            z-index: 1;
            padding: 2rem;
            max-width: 900px;
            /* Animación de entrada para el contenido del héroe */
            animation: fadeInScale 1s ease-out forwards;
            opacity: 0; /* Inicia invisible */
            transform: scale(0.95); /* Ligeramente encogido */
        }

        /* Keyframes para la animación de entrada */
        @keyframes fadeInScale {
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        /* Animación para el botón de llamada a la acción */
        .hero-button {
            transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
        }

        .hero-button:hover {
            transform: scale(1.08); /* Ligeramente más grande al pasar el ratón */
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2); /* Sombra más pronunciada */
        }

        /* Estilos para el menú móvil */
        .mobile-menu {
            transition: transform 0.3s ease-in-out;
            transform: translateX(100%); /* Oculta el menú fuera de la pantalla inicialmente */
        }
        .mobile-menu.is-open {
            transform: translateX(0); /* Desliza el menú a la vista */
        }

        /* Estilos para el carrusel */
        .carousel-slide {
            opacity: 0;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            transition: opacity 0.8s ease-in-out;
            display: flex; /* Asegura que el contenido esté centrado */
            align-items: center;
            justify-content: center;
        }
        .carousel-slide.active {
            opacity: 1;
            position: relative; /* Para que ocupe espacio cuando está activo */
        }
        .carousel-content {
            position: relative;
            z-index: 1;
            padding: 2rem;
            max-width: 900px;
            text-align: center;
        }
        .carousel-indicators button {
            background-color: rgba(255, 255, 255, 0.5);
            width: 10px;
            height: 10px;
            border-radius: 50%;
            margin: 0 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .carousel-indicators button.active {
            background-color: white;
        }
        .carousel-nav-button {
            background-color: rgba(0, 0, 0, 0.5);
            padding: 1rem;
            border-radius: 50%;
            transition: background-color 0.3s ease;
        }
        .carousel-nav-button:hover {
            background-color: rgba(0, 0, 0, 0.8);
        }
    </style>
    <!-- Incluir iconos de Lucide (para un toque moderno) -->
    <script src="https://unpkg.com/lucide@latest"></script>
</head>
<body class="bg-gray-50 text-gray-900 flex flex-col min-h-screen">

    <!-- Encabezado de la Página -->
    <header class="bg-white shadow-lg p-4 sticky top-0 z-10">
        <div class="container mx-auto flex justify-between items-center">
            <!-- Enlace del logo a la página de inicio -->
            <h1 class="text-3xl font-extrabold text-indigo-700">
                <a href="index.html" class="hover:text-indigo-600 transition duration-300">Teknovae</a>
            </h1>
            <!-- Menú de navegación para escritorio -->
            <nav class="hidden md:block">
                <ul class="flex space-x-4">
                    <li><a href="#home" class="text-gray-600 text-sm hover:text-indigo-600 transition duration-300 font-normal">Inicio</a></li>
                    <li><a href="#features" class="text-gray-600 text-sm hover:text-indigo-600 transition duration-300 font-normal">Características</a></li>
                    <li><a href="#products" class="text-gray-600 text-sm hover:text-indigo-600 transition duration-300 font-normal">Productos</a></li>
                    <li><a href="#location" class="text-gray-600 text-sm hover:text-indigo-600 transition duration-300 font-normal">Ubicación</a></li>
                    <li><a href="#about" class="text-gray-600 text-sm hover:text-indigo-600 transition duration-300 font-normal">Sobre Nosotros</a></li>
                    <li><a href="Contacto.html" class="text-gray-600 text-sm hover:text-indigo-600 transition duration-300 font-normal">Contacto</a></li>
                </ul>
            </nav>
            <!-- Botón de menú hamburguesa para móvil -->
            <button id="mobile-menu-button" class="md:hidden p-2 text-gray-600 hover:text-indigo-600 focus:outline-none">
                <i data-lucide="menu" class="w-8 h-8"></i>
            </button>
        </div>
    </header>

    <!-- Menú Móvil (oculto por defecto) -->
    <div id="mobile-menu" class="mobile-menu fixed inset-0 bg-white z-50 flex-col items-center justify-center space-y-8 text-xl hidden">
        <button id="close-mobile-menu" class="absolute top-4 right-4 p-2 text-gray-600 hover:text-indigo-600 focus:outline-none">
            <i data-lucide="x" class="w-8 h-8"></i>
        </button>
        <ul class="flex flex-col space-y-6 text-center">
            <li><a href="#home" class="text-gray-800 hover:text-indigo-600 transition duration-300 font-semibold text-2xl" onclick="closeMobileMenu()">Inicio</a></li>
            <li><a href="#features" class="text-gray-800 hover:text-indigo-600 transition duration-300 font-semibold text-2xl" onclick="closeMobileMenu()">Características</a></li>
            <li><a href="#products" class="text-gray-800 hover:text-indigo-600 transition duration-300 font-semibold text-2xl" onclick="closeMobileMenu()">Productos</a></li>
            <li><a href="#location" class="text-gray-800 hover:text-indigo-600 transition duration-300 font-semibold text-2xl" onclick="closeMobileMenu()">Ubicación</a></li>
            <li><a href="#about" class="text-gray-800 hover:text-indigo-600 transition duration-300 font-semibold text-2xl" onclick="closeMobileMenu()">Sobre Nosotros</a></li>
            <li><a href="Contacto.html" class="text-gray-800 hover:text-indigo-600 transition duration-300 font-semibold text-2xl" onclick="closeMobileMenu()">Contacto</a></li>
        </ul>
    </div>

    <!-- Sección del Banner Principal (Hero) con Carrusel -->
    <section id="home" class="hero-banner relative">
        <div id="carousel-container" class="w-full h-full relative">
            <!-- Slide 1 -->
              <div class="carousel-slide" style="background-image: url('17.webp'); background-size: cover; background-position: center;">
                <div class="carousel-content">
                    <h2 class="text-5xl md:text-7xl font-extrabold mb-4 leading-tight drop-shadow-lg"></h2>
                    <p class="text-lg md:text-xl mb-8 opacity-95 drop-shadow-md">
                    
                   
                </div>
            </div>
            <!-- Slide 2 -->
              <div class="carousel-slide" style="background-image: url('16.webp'); background-size: cover; background-position: center;">
                <div class="carousel-content">
                    <h2 class="text-5xl md:text-7xl font-extrabold mb-4 leading-tight drop-shadow-lg"></h2>
                    <p class="text-lg md:text-xl mb-8 opacity-95 drop-shadow-md">
                      
                    
                </div>
            </div>
            <!-- Slide 3 -->
            <div class="carousel-slide" style="background-image: url('15.webp'); background-size: cover; background-position: center;">
                <div class="carousel-content">
                    <h2 class="text-5xl md:text-7xl font-extrabold mb-4 leading-tight drop-shadow-lg"></h2>
                    <p class="text-lg md:text-xl mb-8 opacity-95 drop-shadow-md">
                     
                   
                </div>
            </div>

            <!-- Botones de Navegación -->
            <button id="carousel-prev" class="carousel-nav-button absolute left-4 top-1/2 -translate-y-1/2 text-white p-3 rounded-full focus:outline-none">
                <i data-lucide="chevron-left" class="w-8 h-8"></i>
            </button>
            <button id="carousel-next" class="carousel-nav-button absolute right-4 top-1/2 -translate-y-1/2 text-white p-3 rounded-full focus:outline-none">
                <i data-lucide="chevron-right" class="w-8 h-8"></i>
            </button>

            <!-- Indicadores de Puntos -->
            <div id="carousel-indicators" class="absolute bottom-6 left-1/2 -translate-x-1/2 flex space-x-2">
                <button class="active"></button>
                <button></button>
                <button></button>
            </div>
        </div>
    </section>

    <!-- Contenido Principal -->
    <main class="container mx-auto p-6 flex-grow">

        <!-- Sección de Características/Productos Destacados -->
        <section id="features" class="mb-20 pt-12">
            <h2 class="text-4xl font-extrabold text-center text-gray-800 mb-12">Nuestras Soluciones Tecnológicas</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
                <!-- Tarjeta de Característica 1 -->
                <div class="bg-white rounded-xl shadow-xl p-8 text-center border border-gray-200 transform hover:translate-y-[-5px] transition duration-300">
                    <i data-lucide="monitor" class="w-16 h-16 text-indigo-600 mx-auto mb-6"></i>
                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Pantallas de Última Generación</h3>
                    <p class="text-gray-600 leading-relaxed">
                        Sumérgete en colores vibrantes y detalles nítidos con nuestros monitores y televisores de alta definición.
                    </p>
                </div>
                <!-- Tarjeta de Característica 2 -->
                <div class="bg-white rounded-xl shadow-xl p-8 text-center border border-gray-200 transform hover:translate-y-[-5px] transition duration-300">
                    <i data-lucide="cpu" class="w-16 h-16 text-indigo-600 mx-auto mb-6"></i>
                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Rendimiento Imparable</h3>
                    <p class="text-gray-600 leading-relaxed">
                        Equipos con procesadores de vanguardia para que tu trabajo y entretenimiento fluyan sin interrupciones.
                    </p>
                </div>
                <!-- Tarjeta de Característica 3 -->
                <div class="bg-white rounded-xl shadow-xl p-8 text-center border border-gray-200 transform hover:translate-y-[-5px] transition duration-300">
                    <i data-lucide="battery-charging" class="w-16 h-16 text-indigo-600 mx-auto mb-6"></i>
                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Autonomía Extendida</h3>
                    <p class="text-gray-600 leading-relaxed">
                        Dispositivos diseñados para acompañarte todo el día, con baterías de larga duración y carga rápida.
                    </p>
                </div>
                <!-- Tarjeta de Característica 4 -->
                <div class="bg-white rounded-xl shadow-xl p-8 text-center border border-gray-200 transform hover:translate-y-[-5px] transition duration-300">
                    <i data-lucide="cloud" class="w-16 h-16 text-indigo-600 mx-auto mb-6"></i>
                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Conectividad Total</h3>
                    <p class="text-gray-600 leading-relaxed">
                        Mantente conectado con la última tecnología Wi-Fi, Bluetooth y 5G para una experiencia fluida.
                    </p>
                </div>
                <!-- Tarjeta de Característica 5 -->
                <div class="bg-white rounded-xl shadow-xl p-8 text-center border border-gray-200 transform hover:translate-y-[-5px] transition duration-300">
                    <i data-lucide="camera" class="w-16 h-16 text-indigo-600 mx-auto mb-6"></i>
                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Fotografía Profesional</h3>
                    <p class="text-gray-600 leading-relaxed">
                        Captura cada momento con cámaras de alta resolución y funciones avanzadas en nuestros smartphones.
                    </p>
                </div>
                <!-- Tarjeta de Característica 6 -->
                <div class="bg-white rounded-xl shadow-xl p-8 text-center border border-gray-200 transform hover:translate-y-[-5px] transition duration-300">
                    <i data-lucide="shield-check" class="w-16 h-16 text-indigo-600 mx-auto mb-6"></i>
                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Seguridad Avanzada</h3>
                    <p class="text-gray-600 leading-relaxed">
                        Protege tu información con características de seguridad de última generación y privacidad garantizada.
                    </p>
                </div>
            </div>
        </section>

        <!-- Sección de Productos -->
        <section id="products" class="mb-20 pt-12">
            <h2 class="text-4xl font-extrabold text-center text-gray-800 mb-12">Nuestros Productos Destacados</h2>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
                <!-- Producto 1 -->
                <div class="bg-white rounded-xl shadow-xl overflow-hidden border border-gray-200 transform hover:scale-105 transition duration-300">
                    <img src="https://placehold.co/400x300/e0e7ff/4338ca?text=Laptop+Pro" alt="Laptop Pro" class="w-full h-48 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">Laptop Ultrabook Pro</h3>
                        <p class="text-gray-600 text-sm mb-4">Diseño elegante, rendimiento excepcional. Perfecta para profesionales.</p>
                        <span class="text-2xl font-bold text-indigo-600">$1,499.99</span>
                    </div>
                </div>
                <!-- Producto 2 -->
                <div class="bg-white rounded-xl shadow-xl overflow-hidden border border-gray-200 transform hover:scale-105 transition duration-300">
                    <img src="https://placehold.co/400x300/d1fae5/065f46?text=Smartphone+X" alt="Smartphone X" class="w-full h-48 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">Smartphone Tek X</h3>
                        <p class="text-gray-600 text-sm mb-4">Cámara de 108MP, batería de 5000mAh y pantalla AMOLED.</p>
                        <span class="text-2xl font-bold text-indigo-600">$799.00</span>
                    </div>
                </div>
                <!-- Producto 3 -->
                <div class="bg-white rounded-xl shadow-xl overflow-hidden border border-gray-200 transform hover:scale-105 transition duration-300">
                    <img src="https://placehold.co/400x300/ffe4e6/be123c?text=Auriculares+ANC" alt="Auriculares ANC" class="w-full h-48 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">Auriculares ANC Pro</h3>
                        <p class="text-gray-600 text-sm mb-4">Cancelación de ruido activa y sonido de alta fidelidad.</p>
                        <span class="text-2xl font-bold text-indigo-600">$189.99</span>
                    </div>
                </div>
                <!-- Producto 4 -->
                <div class="bg-white rounded-xl shadow-xl overflow-hidden border border-gray-200 transform hover:scale-105 transition duration-300">
                    <img src="https://placehold.co/400x300/fff7ed/b45309?text=Smartwatch+Fit" alt="Smartwatch Fit" class="w-full h-48 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">Smartwatch FitMax</h3>
                        <p class="text-gray-600 text-sm mb-4">Monitor de salud completo, GPS y notificaciones inteligentes.</p>
                        <span class="text-2xl font-bold text-indigo-600">$249.50</span>
                    </div>
                </div>
                <!-- Producto 5 -->
                <div class="bg-white rounded-xl shadow-xl overflow-hidden border border-gray-200 transform hover:scale-105 transition duration-300">
                    <img src="https://placehold.co/400x300/e0f2fe/0369a1?text=Tablet+Ultra" alt="Tablet Ultra" class="w-full h-48 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">Tablet Ultra HD</h3>
                        <p class="text-gray-600 text-sm mb-4">Pantalla 4K, procesador ultrarrápido y batería de 10 horas.</p>
                        <span class="text-2xl font-bold text-indigo-600">$599.00</span>
                    </div>
                </div>
                <!-- Producto 6 -->
                <div class="bg-white rounded-xl shadow-xl overflow-hidden border border-gray-200 transform hover:scale-105 transition duration-300">
                    <img src="https://placehold.co/400x300/f0fdf4/16a34a?text=Camara+Web" alt="Camara Web" class="w-full h-48 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">Cámara Web 4K Pro</h3>
                        <p class="text-gray-600 text-sm mb-4">Videollamadas nítidas y streaming de alta calidad.</p>
                        <span class="text-2xl font-bold text-indigo-600">$85.00</span>
                    </div>
                </div>
                <!-- Producto 7 -->
                <div class="bg-white rounded-xl shadow-xl overflow-hidden border border-gray-200 transform hover:scale-105 transition duration-300">
                    <img src="https://placehold.co/400x300/fef2f2/ef4444?text=Router+Mesh" alt="Router Mesh" class="w-full h-48 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">Sistema Wi-Fi Mesh</h3>
                        <p class="text-gray-600 text-sm mb-4">Cobertura total en tu hogar con la última tecnología Wi-Fi 6.</p>
                        <span class="text-2xl font-bold text-indigo-600">$299.00</span>
                    </div>
                </div>
                <!-- Producto 8 -->
                <div class="bg-white rounded-xl shadow-xl overflow-hidden border border-gray-200 transform hover:scale-105 transition duration-300">
                    <img src="https://placehold.co/400x300/eef2ff/4f46e5?text=Drone+Mini" alt="Drone Mini" class="w-full h-48 object-cover">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">Mini Drone Plegable</h3>
                        <p class="text-gray-600 text-sm mb-4">Ideal para principiantes, con cámara HD y fácil manejo.</p>
                        <span class="text-2xl font-bold text-indigo-600">$120.00</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- Sección de Ubicación -->
        <section id="location" class="mb-20 pt-12 bg-white rounded-xl shadow-xl p-10 border border-gray-200 text-center">
            <h2 class="text-4xl font-extrabold text-gray-800 mb-8">Encuéntranos</h2>
            <div class="max-w-xl mx-auto text-lg text-gray-700 space-y-4">
                <p class="flex items-center justify-center space-x-2">
                    <i data-lucide="map-pin" class="w-6 h-6 text-indigo-600"></i>
                    <span>Avenida Siempre Viva 742, Springfield, Anytown, 12345</span>
                </p>
                <p class="flex items-center justify-center space-x-2">
                    <i data-lucide="phone" class="w-6 h-6 text-indigo-600"></i>
                    <span>+1 (555) 123-4567</span>
                </p>
                <p class="flex items-center justify-center space-x-2">
                    <i data-lucide="mail" class="w-6 h-6 text-indigo-600"></i>
                    <span>info@teknovae.com</span>
                </p>
                <div class="pt-4">
                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Horario de Atención:</h3>
                    <p>Lunes a Viernes: 9:00 AM - 7:00 PM</p>
                    <p>Sábados: 10:00 AM - 4:00 PM</p>
                    <p>Domingos: Cerrado</p>
                </div>
            </div>
        </section>

        <!-- Sección Sobre Nosotros -->
        <section id="about" class="bg-white rounded-xl shadow-xl p-10 mb-20 border border-gray-200">
            <h2 class="text-4xl font-extrabold text-center text-gray-800 mb-10">Nuestra Historia y Misión</h2>
            <div class="flex flex-col md:flex-row items-center md:space-x-10">
                <div class="md:w-1/2 mb-8 md:mb-0">
                    <img src="https://placehold.co/600x400/e0e7ff/4338ca?text=Vision+Tecnologica" alt="Visión Tecnológica" class="rounded-lg shadow-md w-full h-auto object-cover">
                </div>
                <div class="md:w-1/2">
                    <p class="text-lg text-gray-700 leading-relaxed mb-4">
                        En **Teknovae**, creemos que la tecnología no solo debe ser funcional, sino también una extensión elegante de tu estilo de vida. Desde nuestra fundación en 2020, nos hemos dedicado a curar una selección exclusiva de dispositivos que combinan innovación, rendimiento y un diseño impecable.
                    </p>
                    <p class="text-lg text-gray-700 leading-relaxed">
                        Nuestra misión es empoderar a nuestros clientes con las herramientas del futuro, ofreciendo productos de la más alta calidad y un servicio excepcional. Cada artículo en nuestro catálogo es elegido por su capacidad de mejorar tu productividad, entretenimiento y conectividad.
                    </p>
                </div>
            </div>
        </section>

        <!-- Sección de Contacto (Formulario en la página principal) -->
        <section id="contact" class="bg-white rounded-xl shadow-xl p-10 border border-gray-200">
            <h2 class="text-4xl font-extrabold text-center text-gray-800 mb-10">Ponte en Contacto</h2>
            <form class="max-w-2xl mx-auto space-y-6">
                <div>
                    <label for="contact-name" class="block text-gray-700 text-lg font-semibold mb-2">Nombre Completo:</label>
                    <input type="text" id="contact-name" name="name" class="shadow-sm appearance-none border border-gray-300 rounded-lg w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Tu Nombre">
                </div>
                <div>
                    <label for="contact-email" class="block text-gray-700 text-lg font-semibold mb-2">Correo Electrónico:</label>
                    <input type="email" id="contact-email" name="email" class="shadow-sm appearance-none border border-gray-300 rounded-lg w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="tu@email.com">
                </div>
                <div>
                    <label for="contact-subject" class="block text-gray-700 text-lg font-semibold mb-2">Asunto:</label>
                    <input type="text" id="contact-subject" name="subject" class="shadow-sm appearance-none border border-gray-300 rounded-lg w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Motivo de tu consulta">
                </div>
                <div>
                    <label for="contact-message" class="block text-gray-700 text-lg font-semibold mb-2">Tu Mensaje:</label>
                    <textarea id="contact-message" name="message" rows="6" class="shadow-sm appearance-none border border-gray-300 rounded-lg w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Escribe aquí tu mensaje..."></textarea>
                </div>
                <div class="flex justify-center">
                    <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-10 rounded-lg shadow-lg transform hover:scale-105 transition duration-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
                        Enviar Mensaje
                    </button>
                </div>
            </form>
        </section>
    </main>

    <!-- Pie de Página -->
    <footer class="bg-gray-900 text-white p-8 mt-16">
        <div class="container mx-auto text-center">
            <p class="text-lg mb-4">&copy; 2024 Teknovae. Todos los derechos reservados.</p>
            <div class="flex justify-center space-x-6 mt-4">
                <a href="#" class="text-gray-400 hover:text-white transition duration-300"><i data-lucide="facebook" class="w-7 h-7"></i></a>
                <a href="#" class="text-gray-400 hover:text-white transition duration-300"><i data-lucide="instagram" class="w-7 h-7"></i></a>
                <a href="#" class="text-gray-400 hover:text-white transition duration-300"><i data-lucide="twitter" class="w-7 h-7"></i></a>
                <a href="#" class="text-gray-400 hover:text-white transition duration-300"><i data-lucide="linkedin" class="w-7 h-7"></i></a>
            </div>
            <p class="text-sm text-gray-500 mt-6">Diseñado con pasión por la tecnología.</p>
        </div>
    </footer>

    <script>
        // Inicializar iconos de Lucide al cargar el DOM
        document.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();

            // Lógica del menú móvil
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const closeMobileMenuButton = document.getElementById('close-mobile-menu');
            const mobileMenu = document.getElementById('mobile-menu');

            mobileMenuButton.addEventListener('click', () => {
                mobileMenu.classList.remove('hidden');
                mobileMenu.classList.add('flex', 'is-open');
            });

            function closeMobileMenu() {
                mobileMenu.classList.remove('flex', 'is-open');
                mobileMenu.classList.add('hidden');
            }
            window.closeMobileMenu = closeMobileMenu; // Hacerla global para los enlaces del menú
            closeMobileMenuButton.addEventListener('click', closeMobileMenu);

            // Lógica del carrusel
            const slides = document.querySelectorAll('.carousel-slide');
            const indicatorsContainer = document.getElementById('carousel-indicators');
            const prevButton = document.getElementById('carousel-prev');
            const nextButton = document.getElementById('carousel-next');
            let currentSlide = 0;
            let slideInterval;

            function showSlide(index) {
                // Ocultar todas las diapositivas
                slides.forEach((slide) => {
                    slide.classList.remove('active');
                });
                // Desactivar todos los indicadores
                Array.from(indicatorsContainer.children).forEach((indicator) => {
                    indicator.classList.remove('active');
                });

                // Mostrar la diapositiva activa
                slides[index].classList.add('active');
                // Activar el indicador correspondiente
                indicatorsContainer.children[index].classList.add('active');
                currentSlide = index;
            }

            function nextSlide() {
                currentSlide = (currentSlide + 1) % slides.length;
                showSlide(currentSlide);
            }

            function prevSlide() {
                currentSlide = (currentSlide - 1 + slides.length) % slides.length;
                showSlide(currentSlide);
            }

            // Crear indicadores dinámicamente (solo si no existen ya)
            if (indicatorsContainer.children.length === 0) {
                slides.forEach((_, index) => {
                    const indicator = document.createElement('button');
                    indicator.addEventListener('click', () => {
                        showSlide(index);
                        resetInterval();
                    });
                    indicatorsContainer.appendChild(indicator);
                });
            }


            // Event listeners para los botones de navegación
            prevButton.addEventListener('click', () => {
                prevSlide();
                resetInterval();
            });
            nextButton.addEventListener('click', () => {
                nextSlide();
                resetInterval();
            });

            // Autoplay del carrusel
            function startInterval() {
                slideInterval = setInterval(nextSlide, 5000); // Cambia cada 5 segundos
            }

            function resetInterval() {
                clearInterval(slideInterval);
                startInterval();
            }

            // Inicializar el carrusel
            showSlide(currentSlide);
            startInterval();
        });
    </script>
</body>
</html>
