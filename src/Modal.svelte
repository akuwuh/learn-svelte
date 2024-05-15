
<script>
    // Props
    export let message = 'default value';
    export let isPromo = false;
    export let showModal = false;

    // Event Modifiers:
    // once -> makes sure that event can only be fired once
    // preventDefault -> prevents default behaviour of the event (e.g form submission)
    // self -> only fires if the event is fired on the element itself, not on a child element

</script>

<!-- Conditionals -->
{#if showModal}
    <!-- class becomes isPromo if isPromo is true -->
    <div class="backdrop" class:promo={isPromo} on:click|self> 
        <div class="modal">

            <!-- Slots -->
            <slot></slot>

        </div>
    </div>
{/if}


<style>
    .backdrop {
        width: 100%;
        height: 100%;
        position: fixed;
        background: rgba(0,0,0,0.8);
    }
    .modal {
        padding: 10px;
        border-radius: 10px;
        max-width: 400px;
        margin: 10% auto;
        text-align: center;
        background: white;
    }

    /* styles for promotional modal */
    .promo .modal{ 
        background: crimson;
        color: white;
    }
</style>