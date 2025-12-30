<script>
    import { fade } from 'svelte/transition'
    import Avatar from './assets/avatar.jpg';

    import AboutMeZh from './lib/zh/AboutMe.svelte';
    import FindMeZh from './lib/zh/FindMe.svelte';
    import LinksZh from './lib/zh/Links.svelte';

    import AboutMeEn from './lib/en/AboutMe.svelte';
    import FindMeEn from './lib/en/FindMe.svelte';
    import LinksEn from './lib/en/Links.svelte';


    const TabsMap = {
        zh: {
            AboutMe : AboutMeZh,
            FindMe : FindMeZh,
            Links : LinksZh,
        },
        en: {
            AboutMe : AboutMeEn,
            FindMe : FindMeEn,
            Links : LinksEn,
        }
    };
    const Tabs = navigator.language.includes("zh") ? TabsMap.zh : TabsMap.en;

    let CurrentTab = 'AboutMe';
    
    let ContainerHeight = 0;
</script>

<main>
    <div class="container" style="height: {ContainerHeight}px">
        <div class="container-wrapper" bind:clientHeight={ContainerHeight}>

            <div class="container-header">
                <img src='{Avatar}' alt="Avatar"/>
                <span>Ailelix (Felix Chen)</span>
            </div>

            <div class="container-main">
                {#each Object.keys(Tabs) as tab}
                    <button
                        class="tab-selection"
                        class:active={CurrentTab === tab}
                        on:click={() => CurrentTab = tab}
                    >
                        {tab}
                    </button>
                {/each}

                {#key CurrentTab}
                    <div class="tab-container" in:fade={{ duration: 400 }}>
                        <svelte:component this={Tabs[CurrentTab]} />
                    </div>
                {/key}
            </div>
            
        </div>
    </div>
</main>

<style>
    :global(html) {
        width: 100%;
        height: 100%;
        font-family: 'Noto Sans SC', sans-serif;
    }

    :global(body) {
        background: url('./assets/background.jpg') no-repeat center fixed;
        background-size: cover;
    }

    .container {
        display: flex;
        flex-direction: column;

        padding: 20px min(20px, 2vw) 20px min(20px, 2vw);
        border-radius: 20px;
        margin: 15vh auto auto auto;

        width: 90vw;
        max-width: 1200px;

        background-color: #1d1d1f;

        transition: height 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        overflow: hidden;
    }
    .container-wrapper {
        display: flow-root;
    }
    .container-header {
        display: flex;
        flex-direction: row;
        align-items: center;

        padding-bottom: 20px;
        border-bottom: #00B294 solid 4px;
        margin-bottom: 1vh;
    }

    img {
        border-radius: 20px;
        width: min(12vw, 8em);
    }

    span {
        padding-left: 20px;

        color: #f2f2f7;
        font-size: min(6vw, 3em);
    }

    .tab-selection {
        padding: 10px;

        border: none;

        margin-right: 10px;

        color: #f2f2f7;
        font-size: min(4vw, 1.2em);

        background-color: #1d1d1f;
        cursor: pointer;
        transition: color 0.5s;
    }
    .tab-selection:hover {
        color: #00B294;
    }
    .tab-selection.active {
        color: #00B294;
    }

    .tab-container {
        padding: 10px 20px 10px 20px;
        margin-top: 1vh;

        border: #f2f2f7 solid 3px;
        border-radius: 10px;
    }
</style>