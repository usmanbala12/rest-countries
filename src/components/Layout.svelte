<div>
    <div class="top-bar">
        <span>Where in the world?</span>
        <div class="display-mode">
            <i class="fa-solid fa-moon" style="color: white; background-color: white;"></i>Dark Mode
        </div>
    </div>
    <slot></slot>
</div>

<style>
    .top-bar {
        display: flex;
        padding-inline: 2.5em;
        background-color: hsl(var(--dark-mode-elements));
        color: hsl(var(--dark-mode-text));
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
</style>