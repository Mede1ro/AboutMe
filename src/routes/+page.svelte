<script>
    // @ts-nocheck

    import { onMount } from "svelte";
    // @ts-ignore
    import Teste from "$lib/Navbar.svelte";

    const gitUser = "Mede1ro";
    let repos = [];
    let repoAv = "";

    /**
     * @type {number}
     */
    let idade;

    onMount(() => {
        const avatar = document.getElementById("avatar");

        fetch(`https://api.github.com/users/${gitUser}`)
            .then((response) => response.json())
            .then((data) => {
                // @ts-ignore
                avatar.src = data.avatar_url;
                repoAv = data.avatar_url;
            })
            .catch((error) =>
                console.error("Erro ao carregar avatar do GitHub:", error),
            );

        fetch(`https://api.github.com/users/${gitUser}/repos`)
            .then((response) => response.json())
            .then((data) => {
                repos = data;
            })
            .catch((error) =>
                console.error(
                    "Erro ao carregar repositórios do GitHub:",
                    error,
                ),
            );

        fetch(`https://api.github.com/repos/${gitUser}/{repo}`)
            .then((response) => response.json())
            .then((data) => {
                const stars = data.stargazers_count;
                console.log(`O repositório tem ${stars} estrelas.`);
            })
            .catch((error) =>
                console.error("Erro ao carregar dados do repositório:", error),
            );

        // Atualiza o relógio a cada segundo
        updateClock(); // Atualiza imediatamente
        const intervalId = setInterval(updateClock, 1000);

        // Calcula a idade e exibe
        idade = calcularIdade(2005, 12);

        return () => clearInterval(intervalId);
    });

    function updateClock() {
        const clockElement = document.getElementById("clock");
        const now = new Date();

        // Converte o horário local para o horário de Brasília (GMT-3)
        const brtOffset = -3; // Fuso horário de Brasília (GMT-3)
        const utc = now.getTime() + now.getTimezoneOffset() * 60000;
        const brtTime = new Date(utc + 3600000 * brtOffset);

        // Obtém horas, minutos e segundos
        let hours = brtTime.getHours();
        const minutes = brtTime.getMinutes().toString().padStart(2, "0");
        const seconds = brtTime.getSeconds().toString().padStart(2, "0");
        const period = hours >= 12 ? "PM" : "AM";

        // Converte horas para o formato 12 horas
        hours = hours % 12;
        hours = hours ? hours : 12; // O horário 0 deve ser 12
        const formattedHours = hours.toString().padStart(2, "0");

        // @ts-ignore
        clockElement.textContent = `${formattedHours}:${minutes}:${seconds} ${period}`;
    }

    // @ts-ignore
    function calcularIdade(anoNasc, mesNasc) {
        const dataAtual = new Date();

        const anoAtual = dataAtual.getFullYear();
        const mesAtual = dataAtual.getMonth() + 1;

        let idade = anoAtual - anoNasc;

        if (mesAtual < mesNasc) {
            idade--; // Se sim, ainda não fez aniversário este ano
        }

        return idade;
    }

    function getLanguageColor(language) {
        const colors = {
            JavaScript: "#f1e05a",
            TypeScript: "#2b7489",
            Python: "#3572A5",
            Java: "#b07219",
            "C++": "#f34b7d",
            "C#": "#178600",
            Ruby: "#701516",
            Go: "#00ADD8",
            PHP: "#4F5D95",
            Swift: "#ffac45",
            Kotlin: "#A97BFF",
            Rust: "#dea584",
            Dart: "#00B4AB",
            HTML: "#e34c26",
            CSS: "#563d7c",
            Shell: "#89e051",
            Perl: "#0298c3",
            "Objective-C": "#438eff",
            Scala: "#c22d40",
            Haskell: "#5e5086",
            Lua: "#000080",
            R: "#198CE7",
            "Vim Script": "#199f4b",
            TeX: "#3D6117",
            Elixir: "#6e4a7e",
            Erlang: "#B83998",
            D: "#ba595e",
            Julia: "#a270ba",
            V: "#4f87c4",
        };

        return colors[language] || "#878787"; // Default color for unknown languages
    }
</script>

<main class="px-96 py-10">
    <section
        id="home"
        class="container mx-auto mt-10 flex flex-row justify-between items-center"
    >
        <div class="mt-16 flex flex-col">
            <h1 class="nome text-9xl tracking-tighter -ml-2 -mt-20">Mede1ro</h1>
            <h4 class="job text-xl tracking-wide">Desenvolvedor Full-Stack</h4>
            <div class="flex flex-row gap-4 mt-2 socials">
                <a class="p-3 rounded-xl" href="/">
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="1.5em"
                        height="1.5em"
                        fill="none"
                        stroke-width="1.5"
                        viewBox="0 0 24 24"
                        aria-hidden="true"
                        aria-labelledby="github icon"
                        color="var(--white)"
                        ><path
                            d="M16 22.0268V19.1568C16.0375 18.68 15.9731 18.2006 15.811 17.7506C15.6489 17.3006 15.3929 16.8902 15.06 16.5468C18.2 16.1968 21.5 15.0068 21.5 9.54679C21.4997 8.15062 20.9627 6.80799 20 5.79679C20.4558 4.5753 20.4236 3.22514 19.91 2.02679C19.91 2.02679 18.73 1.67679 16 3.50679C13.708 2.88561 11.292 2.88561 8.99999 3.50679C6.26999 1.67679 5.08999 2.02679 5.08999 2.02679C4.57636 3.22514 4.54413 4.5753 4.99999 5.79679C4.03011 6.81549 3.49251 8.17026 3.49999 9.57679C3.49999 14.9968 6.79998 16.1868 9.93998 16.5768C9.61098 16.9168 9.35725 17.3222 9.19529 17.7667C9.03334 18.2112 8.96679 18.6849 8.99999 19.1568V22.0268"
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path><path
                            d="M9 20.0267C6 20.9999 3.5 20.0267 2 17.0267"
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path></svg
                    >
                </a>
                <a class="p-3 rounded-xl" href="/">
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="1.5em"
                        height="1.5em"
                        fill="none"
                        stroke-width="1.5"
                        viewBox="0 0 24 24"
                        aria-hidden="true"
                        aria-labelledby="discord icon"
                        color="var(--white)"
                        ><path
                            d="M5.5 16C10.5 18.5 13.5 18.5 18.5 16"
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path><path
                            d="M15.5 17.5L16.5 19.5C16.5 19.5 20.6713 18.1717 22 16C22 15 22.5301 7.85339 19 5.5C17.5 4.5 15 4 15 4L14 6H12"
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path><path
                            d="M8.52832 17.5L7.52832 19.5C7.52832 19.5 3.35699 18.1717 2.02832 16C2.02832 15 1.49823 7.85339 5.02832 5.5C6.52832 4.5 9.02832 4 9.02832 4L10.0283 6H12.0283"
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path><path
                            d="M8.5 14C7.67157 14 7 13.1046 7 12C7 10.8954 7.67157 10 8.5 10C9.32843 10 10 10.8954 10 12C10 13.1046 9.32843 14 8.5 14Z"
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path><path
                            d="M15.5 14C14.6716 14 14 13.1046 14 12C14 10.8954 14.6716 10 15.5 10C16.3284 10 17 10.8954 17 12C17 13.1046 16.3284 14 15.5 14Z"
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path></svg
                    >
                </a>
                <a class="p-3 rounded-xl" href="/">
                    <svg
                        id="Layer_1"
                        data-name="Layer 1"
                        xmlns="http://www.w3.org/2000/svg"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        width="24"
                        height="24"
                        color="#fff"
                        ><defs
                            ><style>
                                .cls-637b8512f95e86b59c57a13a-1 {
                                    fill: none;
                                    stroke: currentColor;
                                    stroke-miterlimit: 10;
                                }
                            </style></defs
                        ><path
                            class="cls-637b8512f95e86b59c57a13a-1"
                            d="M8.5,17c-2.73-.52-4.33-1.56-5-3"
                        ></path><path
                            class="cls-637b8512f95e86b59c57a13a-1"
                            d="M4.5,10c-1.15-1.92-1.7-5.38-1-6,3.1,2.5,6.12,4.09,9,4,0,0,0-5,4-5a4.38,4.38,0,0,1,3,1h3l-1,3a13.47,13.47,0,0,1-4,11c-5,5-13,4-16,0"
                        ></path><path
                            class="cls-637b8512f95e86b59c57a13a-1"
                            d="M5.5,14a7.57,7.57,0,0,1-3-5"
                        ></path></svg
                    >
                </a>
            </div>
        </div>

        <div class="profile rounded-3xl mr-20">
            <img id="avatar" class="rounded-3xl" src="" alt="" />
        </div>
    </section>

    <section
        id="about"
        class="container mx-auto mt-10 grid grid-cols-2 gap-18 items-start"
    >
        <div class="flex flex-col mt-20 max-w-lg">
            <h2 class="text-3xl hidden">Atividade</h2>
            <div class="flex flex-row gap-4 atividade">
                <img class="logo rounded-2xl" src="shark.gif" alt="" />
                <div class="flex flex-col gap-1 ml-3">
                    <h3 class="user text-2xl font-medium">@igoropioides</h3>
                    <h5 class="text-lg">Fetching...</h5>
                    <h5 id="clock" class="text-lg"> </h5>
                </div>
            </div>
        </div>

        <div class="bio mt-16 max-w-lg">
            Olá, meu nome é Igor e tenho <span>{idade}</span> anos. Sou
            desenvolvedor desde <span>2023</span> e comecei minha jornada na
            programação em
            <span>2020</span>. Sou apaixonado por tecnologia e estou
            constantemente em busca de novos conhecimentos e desafios. No meu
            <span
                ><a href="https://github.com/Mede1ro" target="_blank">GitHub</a
                ></span
            >, você encontrará uma coleção dos meus projetos e contribuições.
        </div>
    </section>

    <section id="code" class="container mx-auto mt-40">
        <h1 class="text-center text-3xl mb-6">
            <span class="font-bold" style="color: #1f2937;">code</span>:work
        </h1>
        <div class="repositorios grid grid-cols-2 gap-4 mx-auto max-w-5xl">
            {#each repos as repo (repo.id)}
                <div class="repo rounded-lg w-[490px] h-[140px] p-4 bg-gray-800">
                    <div class="repo-info-user flex items-center gap-2 mt-2">
                        <img
                            class="repoAv w-[25px] h-[25px] rounded-full"
                            src={repoAv}
                            alt=""
                        />
                        <h3 class="repo-user text-base">{gitUser}</h3>
                    </div>
                    <h2 class="repo-info mt-3 ml-1 text-xl font-medium">
                        {repo.name}
                    </h2>
                    <div class="flex flex-row mt-4 ml-1 gap-4 items-center">
                        <p class="language flex items-center">
                            <span
                                class="dot-language w-[10px] h-[10px] rounded-full mr-2"
                                style="background-color: {getLanguageColor(
                                    repo.language,
                                )};"
                            >
                            </span>
                            {repo.language}
                        </p>
                        <div class="flex items-center">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16px" height="16px" fill="none" stroke-width="1.5" viewBox="0 0 24 24" aria-hidden="true" aria-labelledby="star icon" color="var(--text-secondary)"><path d="M8.58737 8.23597L11.1849 3.00376C11.5183 2.33208 12.4817 2.33208 12.8151 3.00376L15.4126 8.23597L21.2215 9.08017C21.9668 9.18848 22.2638 10.0994 21.7243 10.6219L17.5217 14.6918L18.5135 20.4414C18.6409 21.1798 17.8614 21.7428 17.1945 21.3941L12 18.678L6.80547 21.3941C6.1386 21.7428 5.35909 21.1798 5.48645 20.4414L6.47825 14.6918L2.27575 10.6219C1.73617 10.0994 2.03322 9.18848 2.77852 9.08017L8.58737 8.23597Z" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"></path></svg>
                            <p class="ml-2">{repo.stargazers_count}</p>
                        </div>
                    </div>
                </div>
            {/each}
        </div>
    </section>
    
</main>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300..700&display=swap");

    .bio {
        font-family: "Space Grotesk", sans-serif;
        font-size: 18px;
    }

    @keyframes float {
        0% {
            transform: translatey(0px);
        }
        50% {
            transform: translatey(-10px);
        }
        100% {
            transform: translatey(0px);
        }
    }

    .nome::before {
        content: "///";
        position: absolute;
        top: 240px;
        left: 18%;
        font-size: 250px;
        font-weight: 700;
        z-index: -1;
        opacity: 0.25;
        color: transparent;
        -webkit-text-stroke: 2px white;
        letter-spacing: -0.52em;
        -webkit-user-select: none;
        user-select: none;
    }

    .profile img {
        width: 100%;
        height: 100%;
        object-fit: cover; /* Faz com que a imagem cubra o container mantendo sua proporção */
        image-rendering: -webkit-optimize-contrast;
    }

    .profile {
        width: 420px;
        height: 400px;
        background-color: #1c1f2175;
        animation: float 8s infinite;
        object-fit: cover;
    }

    main {
        color: white;
    }

    .socials a:hover {
        cursor: pointer;
        background-color: #1c1f2175;
    }

    .logo {
        width: 125px;
        height: 125px;
    }

    .bio span {
        background-color: #1c2021d2;
        padding: 3px 6px;
        border-radius: 6px;
        font-size: 16px;
    }

    .bio::before {
        content: "@";
        position: absolute;
        top: 520px;
        right: 400px;
        font-size: 250px;
        font-weight: 700;
        z-index: -1;
        opacity: 0.25;
        color: transparent;
        -webkit-text-stroke: 2px white;
        letter-spacing: -0.52em;
        -webkit-user-select: none;
        user-select: none;
    }

    .repositorios {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 20px;
        justify-items: center; /* Centraliza os itens da grid horizontalmente */
    }

    .repo {
        background-color: #1c1f2175;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: start;
        width: 490px;
        height: 140px;
        padding: 1rem;
    }

    .repo-user {
        font-family: "Poppins", sans-serif;
        color: #d9dee0;
    }

    .repo-info {
        font-family: "Space Grotesk", sans-serif;
    }
</style>
