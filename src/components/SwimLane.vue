<template>
    <div class="swim-lane" @mousedown="startDrag">
      <div
        v-for="lane in lanes"
        :key="lane.id"
        class="lane"
        :style="{ top: lane.top + 'px', left: lane.left + 'px', height: lane.height + 'px', width: lane.width + 'px', position: 'absolute' }"
      >
        <h2 class="lane-title">{{ lane.title }}</h2>
        <div class="lane-content">
          <button @click="scrollLeft(lane.id)" class="scroll-button">‹</button>
          <div class="cards" :ref="'cards-' + lane.id">
            <div v-for="(card, index) in lane.cards" :key="index" class="card">
              <img :src="getImagePath(card.imageUrl)" alt="Card Image" class="card-image" />
              <div class="card-name">{{ card.name }}</div>
            </div>
          </div>
          <button @click="scrollRight(lane.id)" class="scroll-button">›</button>
        </div>
      </div>
    </div>
  </template>

<script>
export default {
  name: 'SwimLane',
  props: {
    lanes: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      isDragging: false,
      dragStartX: 0,
      dragStartY: 0,
      dragLane: null
    }
  },
  methods: {
    getImagePath (imageUrl) {
      // Check if the URL is external or internal
      if (imageUrl.startsWith('http')) {
        return imageUrl
      } else {
        return require(`@/assets/${imageUrl}`)
      }
    },
    scrollLeft (laneId) {
      const lane = this.$refs['cards-' + laneId][0]
      lane.scrollBy({ top: 0, left: -240, behavior: 'smooth' })
    },
    scrollRight (laneId) {
      const lane = this.$refs['cards-' + laneId][0]
      lane.scrollBy({ top: 0, left: 240, behavior: 'smooth' })
    },
    startDrag (event) {
      const targetLane = event.target.closest('.lane')
      if (targetLane) {
        this.isDragging = true
        this.dragStartX = event.clientX - targetLane.offsetLeft
        this.dragStartY = event.clientY - targetLane.offsetTop
        this.dragLane = targetLane
        document.addEventListener('mousemove', this.drag)
        document.addEventListener('mouseup', this.endDrag)
      }
    },
    drag (event) {
      if (this.isDragging && this.dragLane) {
        const x = event.clientX - this.dragStartX
        const y = event.clientY - this.dragStartY
        this.dragLane.style.left = `${x}px`
        this.dragLane.style.top = `${y}px`
      }
    },
    endDrag () {
      if (this.isDragging) {
        this.isDragging = false
        document.removeEventListener('mousemove', this.drag)
        document.removeEventListener('mouseup', this.endDrag)
      }
    }
  },
  mounted () {
    const laneMargin = 3 * 96 // 3 inches in pixels (assuming 96 DPI)
    this.lanes.forEach(lane => {
      lane.width = 1000
      lane.height = 450
      lane.top = laneMargin
      lane.left = laneMargin
    })
  }
}
</script>

  <style>
  .swim-lane {
    position: relative;
  }

  .lane {
    height: 500px;
    border: 1px solid #ccc;
    padding: 10px;
    border-radius: 5px;
    cursor: grab;
    box-sizing: border-box;
    background-color: rgba(0,0,0,0);
  }

  .lane:active {
    cursor: grabbing;
  }

  .lane-title {
    font-size: 1.5em;
    margin-bottom: 10px;
  }

  .lane-content {
    display: flex;
    align-items: center;
    gap: 10px;
    justify-content: center;
  }

  .cards {
    display: flex;
    overflow-x: auto;
    scroll-behavior: smooth;
    max-width: calc(100% - 80px);
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
    transition: border 0.3s ease;
  }

  .card {
    flex: 0 0 240px;
    height: 336px;
    margin-right: 10px;
    padding: 0px;
    background-color: #f0f0f0;
    border-radius: 5px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .card:hover {
  border: 2px solid #1122dc;
}

  .card img.card-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .scroll-button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
    border-radius: 5px;
  }

  .scroll-button:focus {
    outline: 2px solid #0056b3;
  }
  </style>
