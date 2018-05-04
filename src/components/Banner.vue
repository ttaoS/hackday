<template>
<div class="carousel">
  <div class="row">
    <div class="col-md-4">
        <h3>Top activities around you:</h3>
    </div>
    <div class="col-md-offset-6 col-md-2">
      <span><a @click="toggle()" style="font-size: 14px">{{isDisplay ? 'Hide' : 'Show'}}</a></span>
    </div>
  </div>

<carousel :per-page="4" :paginationPadding="2">
    <slide v-for="(place,index) in places" :key="index">
       <template>
      <div class="casing">
      <transition name="fade">
        <div class="thumbnail"  v-if="isDisplay">

          <img :src="place.adImageUrl" alt="" style="height: 150px; width:300px">
          <a :href="place.url" target="_blank" class="middle">
            <p class="description">{{place.description}}</p>
            <div class="button">Book Now</div>
          </a>
        </div>
        </transition>
        <div class="caption">
          <h4>{{place.name}}</h4>
          
        </div>
    </div>
      </template>
    </slide>
  </carousel>
</div>
  
</template>

<script>
import { Carousel, Slide } from 'vue-carousel';
import axios from 'axios';
export default {
  name: 'Banner',
  components: {
    Carousel,
    Slide
  },
  props: {
    msg: String
  },
  data: function() {
    return {
      isDisplay: true,
      places: [],
      mockData: [
        {
          name: 'Blue Mountains Day Tour',
          description:
            'No journey to Australia could be complete without exploring the tranquil beauty of the Blue Mountains.',
          url: 'https://bluemountainstoursydney.com.au/',
          adImageUrl:
            'https://bluemountainstoursydney.com.au/wp-content/uploads/2017/12/Blue-Mountains-Tours-Three-Sisters.jpg'
        },
        {
          name: 'Manly Surf Schools',
          description: 'Experience the Australian Beach!',
          url: 'https://manlysurfschool.com/',
          adImageUrl: 'https://manlysurfschool.com/wp-content/uploads/unknown.jpg'
        },
        {
          name: 'SEA LIFE Sydney Aquarium',
          description:
            'One of Sydney’s premier attractions, SEA LIFE Aquarium at Darling Harbour.',
          url: 'https://www.sydneyaquarium.com.au/',
          adImageUrl:
            'https://www.darlingharbour.com//media/2783/sea_life_penguins_thumbnail.jpg'
        },
        {
          name: 'Sydney Harbour Bridge Climb',
          description:
            'Climbing the Sydney Harbour Bridge is exhilarating – and an unforgettable experience, too.',
          url: 'https://www.bridgeclimb.com/',
          adImageUrl:
            'https://www.bridgeclimb.com/wp-content/uploads/2014/04/The-Experience-featured-image-1-800x741.jpg'
        },
        {
          name: 'Rocks Walking Tour',
          description: '90-minute walking tour of The Rocks, in Sydney.',
          url: 'http://www.rockswalkingtours.com.au/',
          adImageUrl:
            'https://media-cdn.tripadvisor.com/media/photo-s/0d/f5/6d/9b/the-rocks-walking-tour.jpg'
        },
        {
          name: 'Oz Jet Boating',
          description:
            'We spin, splash, fishtail, and dash around all of the iconic sights Sydney Harbour.',
          url: 'https://www.ozjetboating.com.au/',
          adImageUrl:
            'https://scontent.cdninstagram.com/vp/9df68e8e1952563c1527533a2b407f69/5B93713D/t51.2885-15/s640x640/sh0.08/e35/30830359_343867989351186_8633288855174250496_n.jpg'
        }
      ]
    };
  },
  created() {
    axios
      .get(`http://localhost:3001/activities`)
      .then(response => {
        // JSON responses are automatically parsed.
        this.places = response.data;
      })
      .catch(() => {
        this.places = this.mockData;
      });
  },
  methods: {
    toggle: function() {
      this.isDisplay = !this.isDisplay;
    }
  }
};
</script>
<style scoped>
.carousel {
  background: #fff;
  padding: 10px 20px 20px 15px;
  position: fixed;
  bottom: 0;
  z-index: 999;
  border-top: 1px solid #ccc;
}
.casing {
  margin: 0 20px;
}
.middle {
  transition: 0.5s ease;
  opacity: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  width: 70%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  text-align: center;
}
.button {
  background-color: #4caf50;
  color: white;
  font-size: 16px;
  padding: 10px 20px;
}
.description {
  color: black;
  text-align: justify;
  font-weight: 600;
  font-size: 14px;
}
.thumbnail {
  position: relative;
}
.thumbnail:hover img {
  opacity: 0.2;
}
.thumbnail:hover .middle {
  opacity: 1;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
