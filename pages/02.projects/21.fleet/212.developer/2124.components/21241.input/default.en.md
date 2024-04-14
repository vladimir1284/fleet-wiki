# EmailInputComponent

### File Location: 
src/lib/components/inputs/EmailInputComponent.svelte

### Description: 
The EmailInputComponent is a reusable Svelte component that renders an email input field with floating label functionality. It uses the FloatingLabelInput component from the flowbite-svelte library and includes an envelope icon from flowbite-svelte-icons.

### Usage
To use the EmailInputComponent, import it into a parent Svelte component and include it within the markup. Pass the necessary props to customize the behavior and appearance of the input field.

```html
<script>
  import EmailInputComponent from '$lib/components/inputs/EmailInputComponent.svelte';
  let form = { email: '' };
  let constraints = { email: { required: true, pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/ } };
  let errors = {};
</script>

<EmailInputComponent
  placeholder="Enter your email"
  constraints={constraints}
  errors={errors}
  bind:form={form}
/>
```

### Props
- **placeholder**: A string that sets the placeholder text for the email input field.
- **constraints**: An object containing validation constraints for the email input field.
- **errors**: An object containing error messages related to the email input field.
- **form**: An object representing the form data, including the email value.

### Styling: 
The component uses Tailwind CSS classes for styling. The FloatingLabelInput component is styled with the outlined style, and the envelope icon is given a width and height of 6 units each.

### Accessibility:
The component includes an aria-invalid attribute that is conditionally set based on whether there are errors associated with the input field. This helps screen readers identify invalid fields.

### Error Handling:
If there are errors associated with the input field, they are displayed below the input in red text.

### Dependencies:
- **flowbite-svelte**: Provides the FloatingLabelInput component.
- **flowbite-svelte-icons**: Provides the EnvelopeSolid icon component.

# NameInputComponent

### File Location: 
src/lib/components/inputs/NameInputComponent.svelte

### Description: 
The NameInputComponent is a reusable input component for capturing names within the Fleet Towit application. It utilizes the FloatingLabelInput component from the Flowbite Svelte library to provide a floating label effect on the input field.

### Usage: 
To use the NameInputComponent, import it into the parent component and include it in the markup. Bind the necessary properties to control the input's behavior and appearance.

```html
<script lang="ts">
  import NameInputComponent from '$lib/components/inputs/NameInputComponent.svelte';
  // ... other imports and setup
</script>

<NameInputComponent
  placeholder="Enter your name"
  constraints={constraints}
  errors={errors}
  bind:form={form}
/>
```

### Props:
- **placeholder**: A string that sets the placeholder text for the input field.
- **constraints**: An object containing validation constraints for the input field.
- **errors**: An object containing error messages related to the input field.
- **form**: An object representing the form data, typically managed by a form handling library.

### Styling: 
The component uses Tailwind CSS classes for styling. The FloatingLabelInput component is styled with the outlined style.

### Accessibility:
The component includes an aria-invalid attribute that is conditionally set based on whether there are errors associated with the input field. This helps screen readers identify invalid fields.

### Error Handling:
If there are errors associated with the input field, they are displayed below the input in red text.

### Dependencies:
- **flowbite-svelte**: Provides the FloatingLabelInput component.

## Unit Testing

A unit test suite has been developed to ensure the functionality and correctness of this Svelte mail input component. The test covers the following scenarios:

1. **Rendering**: Ensures that the component renders without errors.

2. **Input Binding**: Verifies that the input field binds correctly to the specified variable.

3. **Validation**: Tests the validation logic with different email inputs and constraints.

4. **Error Handling**: Checks if the error message is displayed correctly when an invalid email is entered.

To run the unit tests, use your preferred testing framework and configure it to include the Svelte testing library. The test suite file may look like the following:

```javascript
import { render, fireEvent } from '@testing-library/svelte';
import MailInput from './MailInput.svelte';

describe('MailInput Component', () => {
    it('renders without errors', () => {
        const { container } = render(MailInput);
        expect(container).toBeInTheDocument();
    });

    it('binds to the provided variable', async () => {
        const { getByPlaceholderText } = render(MailInput);
        const input = getByPlaceholderText('Insert your email');
        await fireEvent.input(input, { target: { value: 'test@example.com' } });
        expect(input.value).toBe('test@example.com');
    });

    it('validates email input correctly', async () => {
        const { getByPlaceholderText, getByText } = render(MailInput);
        const input = getByPlaceholderText('Insert your email');

        // Test valid email
        await fireEvent.input(input, { target: { value: 'test@example.com' } });
        expect(getByText('test@example.com')).toBeInTheDocument();

        // Test invalid email
        await fireEvent.input(input, { target: { value: 'invalid-email' } });
        expect(getByText('Invalid email format')).toBeInTheDocument();
    });
});
```

Adjust the test suite according to your testing environment and framework.