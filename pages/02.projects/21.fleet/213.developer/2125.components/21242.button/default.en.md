# ButtonComponent
### File Location: 
src/lib/components/buttons/ButtonComponent.svelte

### Description: 
A reusable button component for the Fleet Towit Application.

### Props:
- **styles**: Optional string. Custom CSS classes to apply to the button for styling.
- **onClick** (function): A callback function to execute when the button is clicked.
- **color**: Optional string. It set the color of the button.
- **placeholder**: A string to display on the button.

### Usage:
```html
<script>
  import ButtonComponent from '$lib/components/buttons/ButtonComponent.svelte';

  let handleClick = () => {
    console.log('Submit button clicked');
  };
</script>

<ButtonComponent onClick={handleClick} placeholder="Save Changes" />
```

### Styling:
The component uses Tailwind CSS classes for styling. The FloatingLabelInput component is styled with the outlined style.

### Dependencies:
- **flowbite-svelte**: Provides the Button component.


# SubmitButtonComponent
### File Location: 
src/lib/components/buttons/SubmitButtonComponent.svelte

### Description: 
A reusable submit button component for forms within the Fleet Towit application.

### Props:
- **styles**: Optional string. Custom CSS classes to apply to the button for styling.
- **onClick** (function): Optional. A callback function to execute when the button is clicked.
- **placeholder**: A string to display on the button.
- **loading**: A boolean to set the button in loading state, preventing clicks runs `onClick` function.
- **disabled**: A boolean to set the button in disabled state.
### Usage:
```html
<script>
  import SubmitButtonComponent from '$lib/components/buttons/SubmitButtonComponent.svelte';

  let isLoading = false;
  let handleClick = () => {
    isLoading = true;
    console.log('Submit button clicked');
    setTimeout(() => {isLoading = false}, 3000);
  };
</script>

<SubmitButtonComponent onClick={handleClick} placeholder="Save Changes" loading={isLoading}/>
```

### Styling:
The component uses Tailwind CSS classes for styling. The FloatingLabelInput component is styled with the outlined style.

### Dependencies:
- **flowbite-svelte**: Provides the Button component.

