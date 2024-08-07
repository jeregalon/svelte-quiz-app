<script>
    let  name = '';
    import { goto } from '$app/navigation';
    import image15 from '$lib/images/image15.png';

    async function startQuiz() {
        alert(`Hola ${name}, ¡empezamos!`);
        await goto('/quiz'); // Navega a la ruta '/quiz' después del alerta
    }
</script>

<section class="welcome-section">
    <h1>¡Comprueba tus conocimientos con este Quiz!</h1>
</section>
  
<section class="input-section">
    <input type="text" bind:value={name} placeholder="Ingresa tu nombre">
    <button on:click={startQuiz}>
        Empezar Quiz
    </button>
</section>

<section class="image-section">
    <div class="carrusel">
        <img src={image15} alt="Imagen">
    </div>
</section>

<style>
    main {
      text-align: center;
      padding: 20px;
    }
    input[type="text"] {
      margin-top: 10px;
      padding: 5px;
    }
    button {
      margin-top: 10px;
      margin-left: 5px;
      cursor: pointer;
      transition: transform 0.3s ease-in-out;
    }
    :root {
    --primary-color: #3498db; /* Azul */
    --secondary-color: #2ecc71; /* Verde */
    --font-family: 'Roboto', sans-serif;
    }
    
    h1 {
        font-size: 3rem;
        text-align: center;
        margin-bottom: 1rem;
        color: red;
    }

    input[type="text"], button {
        border: none;
        outline: none;
        padding: 0.5rem;
        font-size: 1rem;
        border-radius: 0.25rem;
    }

    button:hover {
        background-color: var(--secondary-color);
        cursor: pointer;
        transform: scale(1.1);
    }

    .carrusel {
        height: 500px;
        width: 700px;
        margin-bottom: 10px;
    }

    .image-section {
        margin-top: 15px;
    }

    .carrusel img {
        object-fit: cover;
        width:100%;
        height:100%;    
        /* border-radius: 8px;   */
    }

</style>