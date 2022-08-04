<script>
    import Fa from 'svelte-fa';
    import { faMoon, faSun } from '@fortawesome/free-solid-svg-icons'
    let classMode = ''
    let classNote = 'Light Mode'
    const toggleMode = () => {
        if(classMode === 'light-mode'){
            classNote = 'Light Mode'
            return classMode = ''
        }
        else {
            classMode = 'light-mode'
            classNote = 'Dark Mode'
        }
    }
</script>

<div class={classMode}>
    <div class="top-bar">
        <span>Where in the world?</span>
        <div class="display-mode">
            <button on:click={toggleMode}><Fa icon={classMode === 'light-mode' ? faMoon : faSun}/>  {classNote}</button>
        </div>
    </div>
    <slot></slot>
</div>

<style>
    .top-bar {
        display: flex;
        padding-inline: 2.5em;
        background-color: hsl(var(--elements-color));
        align-items: center;
    }
    .top-bar span {
        flex-grow: 1;
        font-size: 2em;
        font-weight: 600;
        padding-block: 0.5em;
    }
    .top-bar .display-mode {
        padding-block: 0.5em;
    }

    .display-mode button {
        width: max-content;
        border: none;
        background-color: hsl(var(--elements-color));
        color: inherit;
        font-family: inherit;
        padding: 0.5em;
        border-radius: 3px;
    }
</style>