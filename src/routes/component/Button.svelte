<script lang="ts">
    import { clsx } from "clsx";
    import { createEventDispatcher } from "svelte";

    export let variant:
        | "primary"
        | "secondary"
        | "success"
        | "info"
        | "warning"
        | "danger" = "primary";
    export let placement: "start" | "end" | "center" = "start";
    export let size: "xs" | "sm" | "md" | "lg" | "xl" | "2xl" = "2xl";
    export let rounded: "xs" | "sm" | "md" | "lg" | "xl" | "2xl" = "xl";
    export let label: string = "Button";
    export let pill: boolean = false;
    export let outline: boolean = true;
    export let onClick: () => void = () => {};
    export let isLoading: boolean = false;

    const dispatch = createEventDispatcher();

    /**
     * Handle click
     */
    const handleClick = () => {
        if ($$props.disabled) return;
        dispatch("click");
        onClick && onClick();
    };
</script>

<button
    type="button"
    {...$$props}
    class={clsx(
        "btn inline-flex items-center ease-in-out gap-1 w-fit min-w-20 px-3 ring-2 hover:opacity-80",
        {
            "bg-blue-500 text-white border border-black": variant === "primary",
            "bg-zinc-500 text-white border border-black":
                variant === "secondary",
            "bg-green-500 text-white border border-black":
                variant === "success",
            "bg-sky-500 text-white border border-black": variant === "info",
            "bg-amber-500 text-black border border-black":
                variant === "warning",
            "bg-red-500 text-white border border-black": variant === "danger",
            "h-7": size === "xs",
            "h-8": size === "sm",
            "h-9": size === "md",
            "h-10": size === "lg",
            "h-11": size === "xl",
            "h-12": size === "2xl",
            "rounded-sm": rounded === "xs",
            rounded: rounded === "sm",
            "rounded-md": rounded === "md",
            "rounded-lg": rounded === "lg",
            "rounded-xl": rounded === "xl",
            "rounded-2xl": rounded === "2xl",
            "bg-blue-400 text-white border border-black":
                variant === "primary" && outline,
            "bg-zinc-400 text-white border border-black":
                variant === "secondary" && outline,
            "bg-green-400 text-white border border-black":
                variant === "success" && outline,
            "bg-sky-400 text-white border border-black":
                variant === "info" && outline,
            "bg-amber-400 text-black border border-black":
                variant === "warning" && outline,
            "bg-red-400 text-white border border-black":
                variant === "danger" && outline,
            "rounded-full": pill,
            "min-w-fit px-2": !label,
            "opacity-50": $$props.disabled || isLoading,
        },
        $$props.class,
    )}
    disabled={isLoading}
    on:click={handleClick}
>
    {#if placement === "start" && !isLoading}
        <i class="uil uil-compress-arrows"></i>
    {/if}
    {#if label}
        {@html label}
    {:else}
        <slot />
    {/if}

    {#if placement === "end" && !isLoading}
        <i class="uil uil-compress-arrows"></i>
    {/if}
</button>
