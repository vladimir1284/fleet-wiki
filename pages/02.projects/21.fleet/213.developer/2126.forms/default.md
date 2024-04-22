# Form Handling

We will be using [SuperForms](https://superforms.rocks/) to manage form handling.

### Client Side form handling.
```html
<script lang="ts">
    import { superForm } from 'sveltekit-superforms/client';

    export let data;
    const { form, errors, constraints, enhance } = superForm(data.form, {
		onUpdated: async ({ form }) => {
			if (form.valid) {
				// Logic to handle sucessfully form submission
			}
		}
	});
    <form method='POST' use:enhace action='/route/to/your/api/endpoint'>
        <input>
    </form>
</script>
```