<template>
    <div>
        <h2>登入</h2>
        <form @submit.prevent="login">
            <input v-model="user.username" placeholder="用戶名" required />
            <input v-model="user.password" type="password" placeholder="密碼" required />
            <button type="submit">登入</button>
        </form>
    </div>
</template>

<script>
import { loginUser } from '../api';

export default {
    data() {
        return {
            user: {
                username: '',
                password: ''
            }
        };
    },
    methods: {
        async login() {
            try {
                console.log('Attempting to log in with user:', this.user);
                const response = await loginUser(this.user);
                console.log('Login successful, response:', response);



                // 將用戶 ID 傳遞到 UserProfile.vue
                console.log('Pushing ID:', response.data.userId);
                this.$router.push(`/user/${response.data.userId}`);
            } catch (error) {
                console.error('Login failed:', error);
                console.log('Error details:', {
                    message: error.message,
                    response: error.response,
                    status: error.response?.status,
                    headers: error.response?.headers,
                    data: error.response?.data
                });
            }
        }
    }
};
</script>
