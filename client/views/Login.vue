<script setup lang="ts">

import {
	Card,
	CardContent,
	CardDescription,
	CardFooter,
	CardHeader,
	CardTitle
} from '@/components/ui/card'

import {
	Alert,
	AlertDescription,
	AlertTitle
} from '@/components/ui/alert'

import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { Label } from '@/components/ui/label'

import { Ban } from 'lucide-vue-next'

import { ref } from 'vue'

import { useApiStore } from '@/stores/api';
const apiStore = useApiStore();

const loginFailed = ref(false);

let password = '';
const onSubmit = async () => {
	apiStore.isPageLoaded = false;

	await apiStore.auth(password);

	if (!apiStore.isAuthed)
	{
		loginFailed.value = true;
		apiStore.isPageLoaded = true;
	}
}

apiStore.isPageLoaded = true;
</script>

<template>

	<div class="flex min-h-svh flex-col items-center justify-center gap-6 bg-background p-6 md:p-10">

		<div class="w-full max-w-sm">
			<img src="@/assets/jb2-logo.png" class="mx-auto w-32 h-32" alt="Cloud">

			<Alert variant="destructive" v-show="loginFailed">
				<Ban class="h-4 w-4"/>
				<AlertTitle>Error</AlertTitle>
				<AlertDescription>
				Invalid API Key. Please try again.
				</AlertDescription>
			</Alert>
		</div>

		<div class="w-full max-w-sm">
			<form @submit.prevent="onSubmit">
				<Card class="w-full max-w-sm">
					<CardHeader class="text-center">
						<CardTitle class="text-2xl">SOON</CardTitle>
						<CardDescription></CardDescription>
					</CardHeader>
					<CardContent class="grid gap-4">
						<div class="grid gap-2">
							<Label for="password">PASSWORD</Label>
							<Input v-model="password" id="password" type="password" required />
						</div>
					</CardContent>
					<CardFooter>
						<Button type="submit" class="w-full">SUBMIT</Button>
					</CardFooter>
				</Card>
			</form>
		</div>
	</div>
</template>
