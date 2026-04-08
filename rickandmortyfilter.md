# Implement Character Filtering with Bulma UI
Objective: Integrate Bulma-styled filter controls into the Vue.js application to filter Rick and Morty characters by Status and Gender via API query parameters.

## UI Layout (Bulma Components)
Container: Use a .field.is-grouped.is-grouped-multiline wrapper to ensure filters wrap nicely on mobile.

Filter Groups: Use .buttons.has-addons for each category to create cohesive toggle groups.

Styling: * Active State: Apply the .is-link or .is-primary class to the currently selected filter.

Default State: Use .is-light for inactive buttons to maintain visual hierarchy.

## Implementation Details
1. Template Structure
Use Bulma's level or columns system to position the filter bars above the character grid:

HTML
<nav class="level">
  <div class="level-left">
    <div class="level-item">
      <p class="subtitle is-5"><strong>Status:</strong></p>
    </div>
    <div class="level-item">
      <div class="buttons has-addons">
        <button class="button is-small">Alive</button>
        <button class="button is-small">Dead</button>
        <button class="button is-small">Unknown</button>
      </div>
    </div>
  </div>
</nav>
2. Logic & State
Reactive Params: Maintain a filters object in your Vue component:

JavaScript
const filters = reactive({
  status: '',
  gender: ''
});
API Integration: Update your fetch function to append these as URLSearchParams.

Example: https://rickandmortyapi.com/api/character/?status=alive&gender=female

## Acceptance Criteria
Responsive Design: Filters must remain accessible and look clean on mobile devices using Bulma’s responsive modifiers.

Dynamic Class Binding: The .is-selected (or specific color class) must toggle based on the current reactive state.

Reset Capability: A "Clear All" button using the .is-danger.is-outlined class to wipe all active query parameters.

Loading State: Buttons should be disabled or show a .is-loading state while the API request is in flight.

## Suggested Component Extra
To make it pop, use a Bulma Tag inside the character cards to show the current status/gender, making it immediately obvious that the filter worked correctly.
