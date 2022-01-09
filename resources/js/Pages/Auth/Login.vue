<template>
    <Head title="Step Up English - Trang quản trị hệ thống"/>
    <div class="grid grid-cols-3">
        <div class="flex items-center justify-center grid-cols-6 min-h-screen bg-indigo-300 col-span-2">
                <div class="mt-8 rounded-lg shadow-xl overflow-hidden">
                    <carousel :items-to-show="1" :autoplay="2000" :wrap-around="true">
                        <slide v-for="slide in slides" :key="slide">
                            <img :src="slide" alt="">
                        </slide>

                        <template #addons>
                            <navigation/>
                            <Pagination />
                        </template>
                    </carousel>
                </div>
        </div>
        <div class="flex items-center justify-center grid-cols-6 min-h-screen bg-indigo-300">
            <div class="w-full max-w-md col-end-6">

                <form class="mt-8 bg-white rounded-lg shadow-xl overflow-hidden p-6" @submit.prevent="login">
                    <logo class="block mx-auto w-full max-w-xs fill-white" height="50"/>
                    <div class="px-10 py-12">
                        <h1 class="text-center text-xl font-bold">Đăng nhập</h1>
                        <h2 class="text-center text-lg">Sử dụng tài khoản email</h2>
                        <div class="mt-6 mx-auto w-24 border-b-2"/>
                        <text-input v-model="form.email" :error="form.errors.email" class="mt-10" label="Email"
                                    type="email"
                                    autofocus autocapitalize="off"/>
                        <text-input v-model="form.password" :error="form.errors.password" class="mt-6" label="Mật khẩu"
                                    type="password"/>
                        <label class="flex items-center mt-6 select-none" for="remember">
                            <input id="remember" v-model="form.remember" class="mr-1" type="checkbox"/>
                            <span class="text-sm">Ghi nhớ</span>
                        </label>
                    </div>
                    <div class="flex px-10 py-4 bg-gray-100 border-t border-gray-100">
                        <loading-button :loading="form.processing" class="btn-indigo ml-auto" type="submit">Đăng nhập
                        </loading-button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import {Head} from '@inertiajs/inertia-vue3'
import Logo from '@/Shared/Logo'
import TextInput from '@/Shared/TextInput'
import LoadingButton from '@/Shared/LoadingButton'
import 'vue3-carousel/dist/carousel.css';
import {Carousel, Slide, Navigation, Pagination} from 'vue3-carousel';

export default {
    components: {
        Head,
        LoadingButton,
        TextInput,
        Logo,
        Carousel,
        Slide,
        Navigation,
        Pagination
    },
    data() {
        return {
            form: this.$inertia.form({
                    email: 'trungnt.tech@stepup.edu.vn',
                    password: 'admin',
                    remember: false,

                }
            ),
            slides: [
                "https://cf.shopee.vn/file/da99353e4c53ce3d002d15281ca29a12",
                "https://cf.shopee.vn/file/9f57e1737f9f4edfaa8723b8143a4928",
                "https://cf.shopee.vn/file/2e8c9f42accec2c336e513ac91c19f30",
                "https://cf.shopee.vn/file/c7b90d07379035cfff16dd0092b18b0a",
                "https://cf.shopee.vn/file/32ca5cb4ef15c3009c261b48a37690f7",
                "https://cf.shopee.vn/file/d940135506644153f85655a4baae6f5d"
            ]
        }
    }
    ,
    methods: {
        login() {
            this.form.post('/login')
        }
        ,
    }
    ,
}
</script>

<style>
.carousel__item {
    min-height: 200px;
    width: 100%;
    background-color: var(--vc-clr-primary);
    color: var(--vc-clr-white);
    font-size: 20px;
    border-radius: 8px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.carousel__slide {
    padding: 10px;
}

.carousel__prev,
.carousel__next {
    box-sizing: content-box;
    border: 5px solid white;
}
.carousel__prev {
    transform: translate(140%, -50%) !important;
}
.carousel__next {
    transform: translate(-140%, -50%) !important;
}
.carousel__prev--in-active,
.carousel__next--in-active {
    display: none;
}
</style>
