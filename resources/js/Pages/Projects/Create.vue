<template>
    <Head title="New Project" />
    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">New Project</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900">
                        <div class="justify-end m-2 p-2">
                            <form @submit.prevent="submit">
                                <div>
                                    <InputLabel for="skill" value="Skill" />
                                    <select
                                        v-model="form.skill_id"
                                        id="skill_id"
                                        name="skill_id"
                                        class="
                                            mt-1
                                            block
                                            w-full
                                            pl-3
                                            pr-10
                                            py-2
                                            text-base
                                            border-gray-300
                                            focus:outline-none focus:ring-indigo-500 focus:border-indigo-500
                                            sm:text-sm
                                            rounded-md
                                        "
                                    >
                                        <option v-for="skill in skills" :key="skill.id" :value="skill.id">{{ skill.name }}</option>
                                    </select>
                                </div>
                                <div>
                                    <InputLabel for="name" value="Name" />

                                    <TextInput
                                        id="name"
                                        type="text"
                                        class="mt-1 block w-full"
                                        v-model="form.name"
                                        required
                                        autofocus
                                        autocomplete="username"
                                    />

                                    <InputLabel for="project_url" value="Url" />

                                    <TextInput
                                        id="project_url"
                                        type="text"
                                        class="mt-1 block w-full"
                                        v-model="form.project_url"


                                    />

                                    <InputError class="mt-2" :message="form.errors.name" />
                                </div>
                                <div>
                                    <InputLabel for="image" value="Image" />

                                    <TextInput
                                        id="image"
                                        type="file"
                                        class="mt-1 block w-full"
                                        @input="form.image = $event.target.files[0]"
                                    />

                                    <InputError class="mt-2" :message="form.errors.image" />
                                </div>

                                <div class="flex items-center justify-end mt-4">
                                    <PrimaryButton class="ml-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                                        Store
                                    </PrimaryButton>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';
import Checkbox from "@/Components/Checkbox.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import InputLabel from "@/Components/InputLabel.vue";
import InputError from "@/Components/InputError.vue";
import TextInput from "@/Components/TextInput.vue";

defineProps({
    skills: Array
})

const form = useForm({
    name: '',
    image: null,
    skill_id: '',
    project_url: '',
});

const submit = () => {
    form.post(route('skills.store'));
};
</script>
