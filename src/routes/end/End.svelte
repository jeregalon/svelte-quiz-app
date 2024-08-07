<script>
    let  name = '';
    import Counter from './Counter.svelte';
    
    // async function startQuiz() {
    //     alert(`Hola ${name}, ¡empezamos!`);
    //     await goto('/quiz'); // Navega a la ruta '/quiz' después del alerta
    // }
</script>

<section class="welcome-section">
    <h1>¡Felicidades. Haz completado el Quiz!</h1>
</section>

<section>
    <Counter />
</section>

<style>
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

</style>