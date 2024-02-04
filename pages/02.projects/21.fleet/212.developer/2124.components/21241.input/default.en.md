# Svelte Mail Input Component Documentation

## Overview

This Svelte component is designed to be used as a part of a larger superform, providing a customizable email input field. It includes a label, input field, and error message display. The component utilizes Svelte and Tailwind CSS for styling and functionality.

## Usage

```html
<Label class="space-y-2">
    <span>Email</span>
    <Input
        class="focus:ring-0 border-blue-500 focus:outline-0 focus:ring-2 focus:ring-blue-500"
        type="email"
        name="email"
        placeholder="Insert your email"
        required
        aria-invalid={$errors.email ? 'true' : undefined}
        bind:value={$form.email}
        {...$constraints.email}
    >
        <EnvelopeSolid slot="left" class="w-4 h-4" />
    </Input>
</Label>
{#if $errors.email}<span class="text-red-600">{$errors.email}</span>{/if}
```

### Props

- **class**: CSS classes for styling.
- **type**: Specifies the type of input (email in this case).
- **name**: Name of the input field.
- **placeholder**: Placeholder text for the input field.
- **required**: Indicates if the input is required.
- **aria-invalid**: ARIA attribute to convey error state to screen readers.
- **bind:value**: Binds the value of the input to a variable.
- **{...$constraints.email}**: Additional constraints for validation.

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