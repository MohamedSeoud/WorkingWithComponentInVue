<template>
<base-card>
  <base-button 
  @click="setSelectedTab('stored-resources')"
  :mode="storedResButtonMode">Stored Resources</base-button>
  <base-button
   @click="setSelectedTab('add-resources')"
   :mode="addResButtonMode">Add Resource</base-button>
</base-card>

<keep-alive>
 <component :is="selectedTab"></component>
</keep-alive>

</template>

<script>
import BaseButton from '../UI/BaseButton.vue'
import BaseCard from '../UI/BaseCard.vue'
import AddResources from './AddResources.vue';
import StoredResources from './StoredResources.vue';
export default {
    data() {
        return{ 
            selectedTab: 'stored-resources',
            storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.org',
        },
      ],
        }
    },
    methods:{
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResources(title, description, url){
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResources(resId){
            const index = this.storedResources.findIndex((res) => res.id === resId);
            this.storedResources.splice(index,1)
        }
    },
    computed:{
        storedResButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat' 
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resources' ? null : 'flat' 
        }

    },
    provide(){
        return {
            resources: this.storedResources,
            addResources:this.addResources,
            removeResources:this.removeResources
        }

    },
    components:{BaseCard, BaseButton, StoredResources, AddResources}
}
</script>