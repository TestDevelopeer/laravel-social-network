<template>
    <div class="w-96 mx-auto">
        <div>
            <div class=" mb-3">
                <input v-model="title" class="w-96 rounded-3xl border p-2 border-slate-300" type="text"
                       placeholder="title">

            </div>
            <div class=" mb-3">
                <textarea v-model="content" class="w-96 rounded-3xl border p-2 border-slate-300"
                          placeholder="content"></textarea>

            </div>
            <div class="flex mb-3 items-center">
                <div>
                    <input @change="storeImage" ref="file" type="file" class="hidden">
                    <a href="#" class="block p-2 w-16 text-center text-sm rounded-3xl bg-sky-500 text-white"
                       @click.prevent="selectFile()">Image</a>
                </div>
                <div>
                    <a v-if="image" @click.prevent="image = null" class="ml-3" href="#">Cancel</a>
                </div>
            </div>
            <div v-if="image">
                <img :src="image.url" alt="preview">
            </div>
            <div>
                <a href="#"
                   class="ml-auto block p-2 w-32 rounded-3xl text-center box-border bg-green-600 text-white hover:bg-white hover:border hover:border-green-600 hover:text-green-600">Publish</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Personal",
    data() {
        return {
            title: '',
            content: '',
            image: null
        }
    },
    methods: {
        selectFile() {
            this.fileInput = this.$refs.file;
            this.fileInput.click();
        },
        storeImage(e) {
            const file = e.target.files[0];
            const formData = new FormData();
            formData.append('image', file);
            axios.post('/api/post/image', formData)
                .then(res => {
                    this.image = res.data.data;
                });
        }
    }
}
</script>

<style scoped>

</style>
