<script setup lang="ts">
import { ComponentObjectPropsOptions, ref } from "vue";

interface Props {
    text: string;
    color: string;
    copied: string;
}

defineProps<ComponentObjectPropsOptions<Props>>({
    text: { type: String, default: "Sample Text" },
    color: { type: String, default: "#909399" },
    copied: { type: String, default: "green" },
});

const isCopied = ref<boolean>(false),
    hoverContent = ref<string>("Copy");



const handleCopyClipboard = (content: string) => {
    if (navigator.clipboard) {
        navigator.clipboard.writeText(content).then(() => {
            isCopied.value = true;
            hoverContent.value = "Copied!";
            setTimeout(() => {
                isCopied.value = false;
                hoverContent.value = "Copy";
            }, 2500);
        }).catch((error) => {
            console.error("Failed to copy text:", error);
        });
    } else {
        console.warn("Clipboard API is not supported.");
    }
};

</script>

<template>
    <div class="copy-text">
        <span>
            {{ text }}
        </span>

        <span class="copy-icon">
            <div class="tooltip" v-if="text !== ''">
                <button class="button" v-if="!isCopied" @click="handleCopyClipboard(text)"
                    aria-label="Copy to clipboard">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1024">
                        <path :fill="color"
                            d="M768 832a128 128 0 0 1-128 128H192A128 128 0 0 1 64 832V384a128 128 0 0 1 128-128v64a64 64 0 0 0-64 64v448a64 64 0 0 0 64 64h448a64 64 0 0 0 64-64z">
                        </path>
                        <path :fill="color"
                            d="M384 128a64 64 0 0 0-64 64v448a64 64 0 0 0 64 64h448a64 64 0 0 0 64-64V192a64 64 0 0 0-64-64zm0-64h448a128 128 0 0 1 128 128v448a128 128 0 0 1-128 128H384a128 128 0 0 1-128-128V192A128 128 0 0 1 384 64">
                        </path>
                    </svg>
                </button>
                <button class="button" v-if="isCopied" aria-label="Text copied">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1024">
                        <path :fill="copied"
                            d="M512 64a448 448 0 1 1 0 896 448 448 0 0 1 0-896m-55.808 536.384-99.52-99.584a38.4 38.4 0 1 0-54.336 54.336l126.72 126.72a38.272 38.272 0 0 0 54.336 0l262.4-262.464a38.4 38.4 0 1 0-54.272-54.336z">
                        </path>
                    </svg>
                </button>
                <span class="tooltiptext">{{ hoverContent }}</span>
            </div>
        </span>
    </div>
</template>

<style scoped lang="scss">
.copy-text {
    cursor: pointer;
    display: flex;
    flex-direction: row;

    span.copy-icon {
        opacity: 0;
        margin-left: 0.2rem;
        font-size: 1rem;
        transition: opacity .2s ease,
            transform .2s ease;
        transform: translate(-10px, 0);

        .button {
            background-color: transparent;
            border: none;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            cursor: pointer;
        }
    }

    &:hover {
        span.copy-icon {
            opacity: 1;
            transition: opacity .2s ease, transform .2s ease;
            transform: translate(0, 0);
        }
    }

    .tooltip {
        position: relative;
        display: inline-block;

    }

    .tooltip .tooltiptext {
        visibility: hidden;
        width: 80px;
        background-color: #555;
        color: #fff;
        text-align: center;
        border-radius: 4px;
        padding: 5px 0;
        position: absolute;
        z-index: 1;
        bottom: 125%;
        left: 50%;
        margin-left: -40px;
        opacity: 0;
        transition: opacity 0.3s;
    }

    .tooltip .tooltiptext::after {
        content: "";
        position: absolute;
        top: 100%;
        left: 50%;
        margin-left: -5px;
        border-width: 5px;
        border-style: solid;
        border-color: #555 transparent transparent transparent;
    }

    .tooltip:hover .tooltiptext {
        visibility: visible;
        opacity: 1;
    }

    svg {
        height: 16px;
        width: 16px;
    }
}
</style>
