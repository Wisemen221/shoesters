<template>
   
<!--
header******
-->
    <!-- changing the background of the header on scroll -->
    <header class="header" :class="change_color ? 'no_background' : 'red_background'">
        <nav class="header_nav flex flex_jc_sb flex_ai_c" :class="change_color ? 'big' : 'small'">
            <!-- logo image -->
            <a href="/" class="header_logo flex flex_ai_c">
                <img aria-label="Shoesters Logo" src="@/assets/images/svg/logo.svg" loading="eager" alt="Shoesters Logo">
            </a>
            <!-- mobile menu button -->
            <a href="#" ref="mobileToggle" @click="toggleOn" class="header_mobile_toggle">
                <span></span>
                <span></span>
                <span></span>
            </a>
            <!-- social media buttons -->
            <div class="header_social_links">
                <a href="https://www.facebook.com/Shoesters/"><i class="fab fa-facebook"></i></a>
                <a href="https://www.instagram.com/shoesters1358/"><i class="fab fa-instagram"></i></a>
            </div>
        </nav>
    </header>
    
</template>

<script>
    import { onUpdated, ref } from 'vue'

    export default {
        props:['toggled','change_color','closing'],
        setup(props,context){
            const mobileToggle = ref(null)
            const toggleOn = ()=>{
                // when mobile menu is toggled it will animate and emit data to parent
                if(!mobileToggle.value.classList.contains('header_open')){
                    mobileToggle.value.classList.add('header_open') //adds the animation class
                    context.emit('open_menu') //sends data if menu isn't opened
                }else{
                    if(props.toggled){
                        mobileToggle.value.classList.remove('header_open') //removes the animation class
                        context.emit('close_menu') //sends data if menu is opened
                    }
                }
            }
            const test = onUpdated(()=>{
                if(props.closing){
                    mobileToggle.value.classList.remove('header_open') //removes the animation class
                    context.emit('closed_for_good') //sends data if menu is close
                }
            })
            return{toggleOn,mobileToggle}
        }
    }
</script>