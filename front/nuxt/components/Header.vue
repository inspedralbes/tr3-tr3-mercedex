<template>
    <div class=" flex justify-between items-center px-20 py-6 ">
        <MercedesLogo class="size-16" />
        <nav
            class="flex justify-center gap-x-10 2xl:gap-x-20 text-white font-semibold [&>a:hover]:text-green-300 [&>a]:transition">
            <NuxtLink to="/modelos">Nuestros modelos</NuxtLink>
            <NuxtLink to="/servicios">Servicios</NuxtLink>
            <NuxtLink to="/tienda">Accesorios</NuxtLink>
            <NuxtLink to="/tecnologia">Tecnología</NuxtLink>
        </nav>

        <div class="flex gap-x-3 text-white [&>a]:transition">
            <NuxtLink to="/questions">
                <HelpIcon />
            </NuxtLink>
            <SelectLanguage />
            <NuxtLink :to="getLoggedIn() ? '' : '/login'">
                <ProfileDropdown />
            </NuxtLink>
            <NuxtLink class="cursor-pointer" v-if="cartIcon" @click="mostrarCarritoModal">
                <CartCount />
            </NuxtLink>
        </div>
        <CartModal :carrito="carrito" :cerrarModal="cerrarModal" />
    </div>
</template>

    <script>
    import CartModal from '@/components/CartModal.vue';
    import { useStores } from '@/stores/counter';
    
    export default {
        data() {
            return {
                cartIcon: false
            }
        },
        watch: {
            '$route': function (to, from) {
                this.cartIcon = to.path === '/tienda';
            }
        },
    
        methods: {
            mostrarCarritoModal() {
                const cart = useStores();
                cart.setCartModal(true);
            },
            getLoggedIn() {
                const store = useStores();
                return store.getLoggedIn();
            }
    
        },
        created() {
            this.cartIcon = this.$route.path === '/tienda';
        }
    }
    </script>