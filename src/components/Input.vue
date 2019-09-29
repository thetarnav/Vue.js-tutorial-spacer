<template>
  <input
      type="text"
      class="search"
      id="search-input"
      placeholder="Search some space stuff"
      autofocus
      @input="handleChange"
    />
</template>

<script>
export default {
  name: 'Input',
  data() {return {
    
  }},
  methods: {
    handleChange (e) {
      this.$emit('input', e.target.value);
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/scss/font-faces';
.search {
  padding: 0 5px;
  margin-top: 25px;
  height: 35px;
  width: 210px;
  border: none;
  background: none;
  border-bottom: 2px solid white;
  text-align: center;
  @include small-info;
  color: white;
  transition: box-shadow .2s;
  &::placeholder {
    color: white;
    transition: opacity .2s;
  }
  &:focus {
    outline: none;
    box-shadow: 0 10px 15px -10px rgba(white, 0.4);
    &::placeholder {
      opacity: 0;
    }
  }
}

@media (min-width: 768px) {
  .search {
    height: 44px;
    width: 280px;
    margin-top: 30px;
  }
}
</style>