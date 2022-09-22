<script lang="ts" context="module">
	import axios from 'axios';

	export let baseURL = 'http://localhost:1337';

	const axiosAPI = axios.create({
		baseURL: `${baseURL}`
	});

	const apiRequest = (method: string, url: string) => {
		const headers = {
			Authorization: `Bearer ${import.meta.env.VITE_BEARER_TOKEN}`
		};
		return axiosAPI({
			method,
			url,
			headers
		})
			.then((res) => {
				return Promise.resolve(res.data);
			})
			.catch((err) => {
				return Promise.reject(err);
			});
	};

	const get = (url: string) => apiRequest('get', url);

	export const getEntries = async (endpoint: string) => {
		try {
			const res = await get(endpoint);
			return res.data;
		} catch (error) {
			console.error(error);
		}
	};
</script>
