<template>
  <div class="col-md-6 mx-auto">
    <div class="input-group">
      <input type="search" class="form-control form-control-lg" name="search" @input="getItems" placeholder="Search" aria-label="Search">
      <div class="input-group-append">
        <button class="btn btn-lg btn-success" type="submit">
          <i class="fas fa-search"></i>
        </button>
      </div>
    </div>

    <span v-show="isLoaded">
      <div v-if="!error">
        <div 
          v-for="item of items" 
          :key="item.id"
        >
          <div class="card shadow-sm mt-2">
            <div class="card-body">
              <div class="d-flex align-items-center">
                <img :src="item.img" class="rounded mr-2">
                <h5>{{ item.title }}</h5>
              </div>
              <span class="text-muted">
                <i class="far fa-eye"></i>
                {{ item.views }}
              </span>
            </div>
            <a class="stretched-link" :href="item.alias"></a>
          </div>
        </div>
      </div>
      <div v-else class="mt-2">
        {{ error }}
      </div>
    </span>
  </div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      error: null,
      isLoaded: false,
      items: []
    }
  },
  methods: {
    getItems() {
      if (event.target.value.trim()) {
        fetch('/api/search?q=' + event.target.value.trim())
        .then(res => res.json())
        .then(res => {
          this.items = res.data;
          this.error = null;
        })
        .catch(() => {
          this.error = 'Too many requests';
        });

        this.isLoaded = true;
      } else {
        this.isLoaded = false;
      }
    }
  }
}
</script>

<style scoped>
button {
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

img {
  max-height: 30px;
  max-width: 60px;
}

.form-control {
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}
</style>