<template>
    <div class="entradas">
        <div class="direccion-texto">
            <p>Código</p>
            <input class="entrada-texto" id="email" type="text" v-model="form.email" required autofocus autocomplete="username">
        </div>
        <div class="direccion-texto">
            <div class="texto-combinado">
                <p>Contraseña</p>
            </div>
            <input class="entrada-texto" id="password" type="password" v-model="form.password" required autocomplete="current-password">
        </div>
        <div class="direccion-texto">
            <label class="flex items-center">
                <Checkbox name="remember" v-model:checked="form.remember" />
                <span class="ms-2 text-sm text-gray-600">Remember me</span>
            </label>
        </div>
        <div class="direccion-texto">
            <button class="boton" type="submit" :disabled="form.processing">Iniciar Sesión</button>
            <Link href="/register">Registrarse</Link>
            <Link href="/">Ingresar como invitado</Link>
            <span v-if="errors">{{ errors }}</span>
        </div>
    </div>
</template>

<script setup>
import { useForm } from '@inertiajs/vue3';
import { defineProps } from 'vue';
import Checkbox from '@/Components/Checkbox.vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
    errors: String,
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<style scoped>
p, label, span {
    color: white;
    margin-top: 25px;
}
a {
    text-decoration: none;
    color: white;
    margin-top: 18px;
    font-size: 18px;
}
a:hover {
    color: #E6D9AA;
}
.texto-combinado {
    align-items: baseline;
    text-decoration: none;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}
.direccion-texto {
    display: flex;
    flex-direction: column;
    margin-top: 20px;
}
.entrada-texto {
    height: 50px;
    border-radius: 10px;
    outline: none;
    font-size: 25px;
    border: none;
}
button {
    background-color: #E6D9AA;
    color: #711610;
    font-weight: bold;
    font-size: 25px;
    margin-top: 25px;
    border-radius: 10px;
    border: none;
    height: 50px;
    cursor: pointer;
}
</style>
