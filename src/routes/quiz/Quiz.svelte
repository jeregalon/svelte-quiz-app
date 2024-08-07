 <script>
    import image1 from '$lib/images/image1.jpg';
    import image2 from '$lib/images/image2.jpg';
    import image3 from '$lib/images/image3.jpg';
    import image4 from '$lib/images/image4.jpg';
    import image5 from '$lib/images/image5.jpg';
    import image6 from '$lib/images/image6.jpg';
    import image7 from '$lib/images/image7.jpg';
    import image8 from '$lib/images/image8.jpg';
    import image9 from '$lib/images/image9.png';
    import image10 from '$lib/images/image10.jpg';
    import image11 from '$lib/images/image11.jpg';
    import image12 from '$lib/images/image12.webp';
    import image13 from '$lib/images/image13.webp';
    import image14 from '$lib/images/image14.jpeg';

    import { goto } from '$app/navigation';
    import { rightQuest } from '../../stores';
	import { wrongQuest } from '../../stores';

    rightQuest.set(0);
    wrongQuest.set(0);

    let images = [image1, image2, image3, image4, image5, image6, image7,
        image8, image9, image10, image11, image12, image13, image14
    ];

    const questions = [
        {
            question: "¿Cuál es la capital de Francia?",
            answers: [
                { text: "Berlín", correct: false },
                { text: "Madrid", correct: false },
                { text: "París", correct: true },
                { text: "Lisboa", correct: false }
            ]
        },
        {
            question: "¿Qué es el ADN?",
            answers: [
                { text: "Ácido desoxirribonucleico", correct: true },
                { text: "Ácido ribonucleico", correct: false },
                { text: "Proteína", correct: false },
                { text: "Carbohidrato", correct: false }
            ]
        },
        {
            question: "¿Cuál es el océano más grande del mundo?",
            answers: [
                { text: "Atlántico", correct: false },
                { text: "Índico", correct: false },
                { text: "Ártico", correct: false },
                { text: "Pacífico", correct: true }
            ]
        },
        {
            question: "¿Cuál es el animal más grande del mundo?",
            answers: [
                { text: "Elefante", correct: false },
                { text: "Ballena azul", correct: true },
                { text: "Jirafa", correct: false },
                { text: "Oso polar", correct: false }
            ]
        },
        {
            question: "¿Quién pintó la Mona Lisa?",
            answers: [
                { text: "Pablo Picasso", correct: false },
                { text: "Salvador Dalí", correct: false },
                { text: "Leonardo da Vinci", correct: true },
                { text: "Vincent van Gogh", correct: false }
            ]
        },
        {
            question: "¿Quién escribió 'Cien años de soledad'?",
            answers: [
                { text: "Gabriel García Márquez", correct: true },
                { text: "Julio Cortázar", correct: false },
                { text: "Pablo Neruda", correct: false },
                { text: "Mario Vargas Llosa", correct: false }
            ]
        },
        {
            question: "¿Cuál es el río más largo del mundo?",
            answers: [
                { text: "Nilo", correct: true },
                { text: "Amazonas", correct: false },
                { text: "Misisipi-Misuri", correct: false },
                { text: "Yangtsé", correct: false }
            ]
        },
        {
            question: "¿Quién escribió 'Hamlet'?",
            answers: [
                { text: "William Shakespeare", correct: true },
                { text: "Oscar Wilde", correct: false },
                { text: "Jane Austen", correct: false },
                { text: "Charles Dickens", correct: false }
            ]
        },
        {
            question: "¿Cuál es el planeta más grande del sistema solar?",
            answers: [
                { text: "Saturno", correct: false },
                { text: "Júpiter", correct: true },
                { text: "Urano", correct: false },
                { text: "Neptuno", correct: false }
            ]
        },
        {
            question: "¿Quién fue el primer presidente de los Estados Unidos?",
            answers: [
                { text: "Abraham Lincoln", correct: false },
                { text: "Thomas Jefferson", correct: false },
                { text: "George Washington", correct: true },
                { text: "John Adams", correct: false }
            ]
        },
        {
            question: "¿Cuál es el gas más abundante en la atmósfera terrestre?",
            answers: [
                { text: "Oxígeno", correct: false },
                { text: "Dióxido de carbono", correct: false },
                { text: "Nitrógeno", correct: true },
                { text: "Argón", correct: false }
            ]
        },
        {
            question: "¿Quién descubrió la penicilina?",
            answers: [
                { text: "Marie Curie", correct: false },
                { text: "Albert Einstein", correct: false },
                { text: "Alexander Fleming", correct: true },
                { text: "Louis Pasteur", correct: false }
            ]
        },
        {
            question: "¿Cuál es el instrumento musical de cuerda más grande?",
            answers: [
                { text: "Violín", correct: false },
                { text: "Viola", correct: false },
                { text: "Chelo", correct: false },
                { text: "Contrabajo", correct: true }
            ]
        },
        {
            question: "¿Quién escribió 'El Principito'?",
            answers: [
                { text: "Antoine de Saint-Exupéry", correct: true },
                { text: "Gabriel García Márquez", correct: false },
                { text: "Julio Cortázar", correct: false },
                { text: "Jorge Luis Borges", correct: false }
            ]
        }
    ];

    let currQuest = 0;

    let ansClicked = [false, false, false, false];

    let anyAnsClicked = false;

    let quizFinish = false;
    
    let textButtonNext = "Siguiente";

    function nextQuest() {
        if (currQuest < questions.length - 1) {
            currQuest++;
            if (currQuest === questions.length - 1) {
                textButtonNext = "Finalizar";
            }
        } else {
            quizFinish = true
            console.log(quizFinish);
            goto('/end');
        }
        
        ansClicked = [false, false, false, false];
        anyAnsClicked = false;
    }

</script>

<h1 id="pregunta" >
    {questions[currQuest].question}
</h1>

<div class="carrusel">
    <img src={images[currQuest]} alt="Imagen">
</div>

<div class="button-container">
    {#each questions[currQuest].answers as answer, index}
        <button
            class:neutral={!ansClicked[index]}
            class:correct={answer.correct === true && ansClicked[index]}
            class:incorrect={answer.correct === false && ansClicked[index]}
            on:click={() => {
                ansClicked[index] = true
                anyAnsClicked = true
                if (answer.correct) {
                    rightQuest.update((n) => n + 1);
                    console.log(rightQuest);
                } else {
                    wrongQuest.update((n) => n + 1);
                    console.log(wrongQuest);
                }
            }}
            disabled={anyAnsClicked}
        >
            {answer.text}
        </button>
    {/each}
</div>

<button
    class="next"
    on:click={nextQuest}
    disabled={!anyAnsClicked}
>
    {textButtonNext}
</button>

<style>
    .button-container {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        justify-content: center;
        height: 180px;
        width: 750px;
    }

    .carrusel {
        height: 300px;
        width: 700px;
        margin-bottom: 10px;
    }

    .neutral, .correct, .incorrect {
        height: 80px;
        width: 350px;
        cursor: pointer;
        padding: 5px;
        margin: 5px;
        font-size: 18px;
        border: none; /* Sin borde */
        border-radius: 8px; /* Bordes redondeados */
        color: #6a11cb; /* Color del texto de los botones */
        transition: background-color 0.3s, transform 0.3s; /* Transiciones suaves */
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); /* Sombra */
    }

    .neutral {
        background-color: #ffffff; /* Color de fondo de los botones */
    }

    .correct {
        background-color: #a8e6cf;
        transform: translateY(-2px); /* Efecto de elevación */
    }

    .incorrect {
        background-color: #ff8b8b;
        transform: translateY(-2px); /* Efecto de elevación */
    }

    .neutral:hover {
        background-color: #f0f0f0; /* Color de fondo al pasar el mouse */
        transform: translateY(-2px); /* Efecto de elevación */
    }

    .correct:hover {
        background-color: #a8e6cf;
    }

    .incorrect:hover {
        background-color: #ff8b8b;
    }

    .neutral:active {
        transform: translateY(0); /* Efecto al hacer clic */
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2); /* Sombra al hacer clic */
    }

    .next {
        background-color: #4CAF50; /* Color de fondo verde */
        color: white; /* Color del texto */
        border: none; /* Sin borde */
        padding: 15px 32px; /* Espaciado interno */
        text-align: center; /* Alineación del texto */
        text-decoration: none; /* Sin subrayado */
        display: inline-block; /* Para que se comporte como un botón */
        font-size: 20px; /* Tamaño de la fuente */
        margin: 4px 2px; /* Margen alrededor del botón */
        cursor: pointer; /* Cambiar el cursor al pasar el ratón */
        border-radius: 8px; /* Bordes redondeados */
        transition: background-color 0.3s, transform 0.2s; /* Transición suave */
    }

    .next:hover {
        background-color: #45a049; /* Color de fondo al pasar el ratón */
        transform: scale(1.05); /* Aumentar ligeramente el tamaño */
    }

    .next:active {
        transform: scale(0.95); /* Efecto de pulsar el botón */
    }

    .carrusel img {
        object-fit: cover;
        width:100%;
        height:100%;    
        border-radius: 8px; /* Bordes redondeados */   
    }

</style>

