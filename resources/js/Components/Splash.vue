<template>
    <div class="splash">
        <div class="splash-content">
            <!-- Your splash screen content goes here -->
            <h1>Welcome</h1>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Splash',
}
</script>

<style scoped>
.splash {
    color: #fff;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: #0f1333;
    display: flex;
    justify-content: center;
    align-items: center;
}

.splash-content {
    text-align: center;
}
</style>
