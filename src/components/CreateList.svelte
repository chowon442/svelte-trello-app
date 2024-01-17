<script>
    import { tick } from "svelte";
    import { lists } from "~/store/list";

    let isEditMode = false;
    let title = "";
    let textareaEl;

    function addList() {
        if (title.trim()) {
            lists.add({
                title,
            });
        }
        offEditMode();
    }

    async function onEditMode() {
        isEditMode = true;
        await tick();
        textareaEl && textareaEl.focus();
    }
    function offEditMode() {
        isEditMode = false;
        title = "";
    }
</script>

<div class="create-list">
    {#if isEditMode}
        <div class="edit-mode">
            <textarea
                bind:value={title}
                bind:this={textareaEl}
                placeholder="Enter a title for this list..."
                on:keydown={(event) => {
                    event.key === "Enter" && addList();
                    event.key === "Escape" && offEditMode();
                    event.key === "Esc" && offEditMode();
                }}
            ></textarea>
            <div class="actions">
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <div class="btn success" on:click={addList}>Add List</div>
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <div class="btn" on:click={offEditMode}>Cancel</div>
            </div>
        </div>
    {:else}
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div
            class="add-another-list"
            on:click={onEditMode}
            role="button"
            tabindex="0"
        >
            + Add another list
        </div>
    {/if}
</div>

<style lang="scss">
    .create-list {
        white-space: normal;
        font-size: 16px;
        display: inline-block;
        width: 290px;
        padding: 10px 8px;
        vertical-align: top;
        background: rgba(#ebecf0, 0.6);
        border-radius: 4px;
        margin: 0 4px;
        line-height: 20px;
        cursor: pointer;
        transition: 0.2s;
        &:hover {
            background: #ebecf0;
        }
    }
</style>
