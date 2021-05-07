<template>
    <div class="loader">
        <div class="bar">
            <div class="bar-slide"></div>
        </div>
        <div class="text">Loading <span id="point-1">.</span><span id="point-2">.</span><span id="point-3">.</span></div>
    </div>
</template>

<script>
export default {
    name: 'Loader',
}
</script>

<style scoped lang="scss">
    .loader{
        position: fixed;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        text-align: center;
        letter-spacing: 2px;

        .bar{
            position: relative;
            width: 200px;
            height: 20px;
        }
        .bar-slide{
            position: absolute;
            top: 0;
            left: 0;
            width: 15%;
            height: 100%;
            margin-bottom: 10px;
            background: linear-gradient(90deg, rgba(255,255,255,0) 0%, rgba(255,255,255,1) 100%);  
            animation: slide 1.5s linear infinite;
        }
    }
    .text{
        font-size: 1.5rem;
        #point-1{
            animation: view1 2s linear infinite;
        }
        #point-2{
            opacity: 0;
            animation: view2 2s .5s linear infinite;
        }
        #point-3{
            opacity: 0;
            animation: view3 2s 1s linear infinite;
        }
    }
    @keyframes view1 {
        from, 75%{
            opacity: 1;
        }
        76%,99%{
            opacity: 0;
        }
    }
    @keyframes view2 {
        from, 50%{
            opacity: 1;
        }
        51%,99%{
            opacity: 0;
        }
    }
    @keyframes view3 {
        from, 25%{
            opacity: 1;
        }
        26%,99%{
            opacity: 0;
        }
    }
    @keyframes slide {
        47%{
            transform: rotateY(0);
        }
        50%{
            left: 85%;
            transform: rotateY(180deg);
        }
        97%{
            transform: rotateY(180deg);
        }
        to{
            left: 0;
            transform: rotateY(0);
        }
    }
</style>