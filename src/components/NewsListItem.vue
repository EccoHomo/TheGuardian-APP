<template>
    <div>
        <div class="card-body">
            <h5 class="card-title">
                <a :href="'https://www.theguardian.com/' + news.id"
                    class="card-link"
                    target="_blank">
                    {{ news.webTitle }}
                </a>
            </h5>
            <h6 class="card-subtitle mb-2 text-muted">
                {{ news.pillarName }} > {{ news.sectionName }} | {{ news.webPublicationDate | formatDate }}
            </h6>
        </div>
    </div>
</template>

<script>
export default {
  name: 'NewsListItem',
  props: ['news']
};
</script>