<template>
  <div>
    <MobileSearch></MobileSearch>
    <MobileSearchResults></MobileSearchResults>
  </div>
</template>

<script>
  import MobileSearch from './mobile-search/MobileSearch';
  import MobileSearchResults from './MobileSearchResults';

  export default {
    components: {
      MobileSearch,
      MobileSearchResults
    }
  }
</script>
