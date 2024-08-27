<script>
    // @ts-nocheck
    
    import { onMount } from 'svelte';
    
    onMount(() => {
        const navList = document.getElementById('nav-list');
        const navBar = document.getElementById('nav-bar');
    
        if (navList && navBar) {
            window.addEventListener('scroll', () => {
                if (window.scrollY > 0) {
                    navList.style.transition = 'background-color 0.5s ease';
                    navList.style.backgroundColor = '#191c1fca';
                    navBar.classList.remove('w-3/6');
                    navBar.classList.add('w-2/6');
                    navList.classList.remove('p-4');
                    navList.classList.add('p-3');
                } else {
                    navList.style.backgroundColor = 'transparent'; 
                    navBar.classList.remove('w-2/6');
                    navBar.classList.add('w-3/6');
                    navList.classList.add('p-4');
                    navList.classList.remove('p-3');
                }
            });
        }
    });
</script>

<nav class="p-1 sticky top-0 z-50 transition-all duration-500">
    <div id="nav-bar" class="w-3/6 mx-auto py-2 transition-all duration-800">
        <ul id="nav-list" class="container-sm flex justify-center space-x-6 gap-10 rounded-2xl transition-all duration-800">
            <li class="rounded-full">
                <a class="py-4 px-8 flex items-center justify-center text-center rounded-full text-white text-xl" href="/faz">/</a>
            </li>
            <li class="rounded-full">
                <a class="py-4 px-8 flex items-center justify-center text-center rounded-full text-white text-xl" href="/">about</a>
            </li>
            <li class="rounded-full">
                <a class="py-4 px-8  flex items-center justify-center text-center rounded-full text-white text-xl" href="/">repos</a>
            </li>
        </ul>
    </div>
</nav>

<style>


    a:hover {
        background: rgba(115, 121, 123, .227);
        cursor: pointer;
    }
</style>
