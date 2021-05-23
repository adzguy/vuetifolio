<template>
  <div class="col mb-4">
    <b-card class="h-100">
      <b-card-text>
        <h3>{{ project.name }}</h3>
        <p>{{ project.description }}</p>
        <h5>Updated at</h5>
        <div>{{ new Date(project.updated_at).toDateString() }}</div>
        <b-avatar :src="project.owner.avatar_url" size="6em"></b-avatar>
      </b-card-text>

      <template #footer>
        <small class="text-muted">
          <div>
            <b-button
              :href="project.html_url"
              target="_blank"
              pill
              variant="outline-secondary"
            >
              Code
            </b-button>
          </div>
        </small>
      </template>
    </b-card>
  </div>
</template>

<script>
export default {
  props: ["project"],
};
</script>


