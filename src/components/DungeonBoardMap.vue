<template>
  <div class="mapContainer" >
    <div class="map">
      <div v-for="(row, y) in visibleMap.coordinates" class="mapRow" >
        <div v-for="(cell, x) in row"
             :class="['mapCell',
                     {'darkness': hero.position.x + 3 < x || hero.position.x - 3 > x ||  hero.position.y + 3 < y || hero.position.y - 3 > y },
                     {'hero': hero.position.x === x && hero.position.y === y},
                     {'wall': cell.type === 'wall'}]">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  created: function () {
    window.addEventListener('keydown', this.move);
   },
  data: function() {
    return {
      map: {
        coordinates: [],
        length: {
          y: 40,
          x: 50
        },
        shift: {
          y: 10,
          x: 10
        }
      },
      visibleMap: {
        coordinates: [],
        length: {
          y: 11,
          x: 28
        }
      },
      cellTypes: [
        {
          type: 'ground',
          props: {
            obstacle: false
          }
        },
        {
          type: 'wall',
          props: {
            obstacle: true
          }
        },
        {
          type: 'enemy',
          props: {
            obstacle: true
          }
        },
        {
          type:'potion',
          props: {
            obstacle: false
          }
        }
      ],
      hero: {
        health: 100,
        attack: 10,
        position: {
          y: 6,
          x: 14
        }
      }
    }
  },
  mounted() {
    this.map.coordinates = this.generateMap(this.map.length.y, this.map.length.x);
    this.fillMapWithCellTypes();

    this.visibleMap.coordinates = this.generateMap(this.visibleMap.length.y, this.visibleMap.length.x);
    this.fillVisibleMapWithCoordinates();
  },
  methods: {
    generateMap(rows, cells) {
      let mapCoordinates = [];
      for(let y = 0; y <= rows; y++){
        mapCoordinates.push([]);
        mapCoordinates[y] = new Array(cells);
      }
      return mapCoordinates;
    },
    fillMapWithCellTypes() {
      for(let y = 0; y <= this.map.length.y; y++) {
        for(let x = 0; x <= this.map.length.x; x++) {
          if(x === this.hero.position.x + this.map.shift.y && y === this.hero.position.y + this.map.shift.x) {
            this.map.coordinates[y][x] = this.cellTypes[0];
          } else {
            const randomIdx = Math.floor(this.cellTypes.length * Math.random());
            this.map.coordinates[y][x] = this.cellTypes[randomIdx];
          }
        }
      }
    },
    fillVisibleMapWithCoordinates() {
      let visibleMapRows;
      for(let y = 0; y <= this.visibleMap.length.y; y++) {
        visibleMapRows = this.visibleMap.coordinates[y];
        for(let x = 0; x <= this.visibleMap.length.x; x++) {
          visibleMapRows[x] = this.map.coordinates[y + this.map.shift.y][x + this.map.shift.x];
        }
      }
      this.visibleMap.coordinates.splice(0, visibleMapRows);
    },
    move(event) {
      const heroPosition = Object.assign({}, this.hero.position);
      switch(event.keyCode) {
        case 37:
          heroPosition.x -= 1;
          break;
        case 38:
          heroPosition.y -= 1;
          break;
        case 39:
          heroPosition.x += 1;
          break;
        case 40:
          heroPosition.y += 1;
          break;
      }
      if(this.visibleMap.coordinates[heroPosition.y][heroPosition.x].type === 'wall') {
        //dont move
      } else if(heroPosition.x < 2) {
        this.map.shift.x -= 1;
        this.fillVisibleMapWithCoordinates();
      } else if(heroPosition.x > 26) {
        this.map.shift.x += 1;
        this.fillVisibleMapWithCoordinates();
      } else if(heroPosition.y < 2) {
        this.map.shift.y -= 1;
        this.fillVisibleMapWithCoordinates();
      } else if(heroPosition.y > 9) {
        this.map.shift.y += 1;
        this.fillVisibleMapWithCoordinates();
      } else {
        this.hero.position = heroPosition;
      }
    }
  }
}
</script>

<style scoped>
  .mapContainer {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    grid-template-areas:
      '. map .';
  }
  .map {
    grid-area: map;
  }
  .mapRow {
    display: grid;
    grid-template-columns: repeat(29, 32px);
  }
  .mapCell {
    height: 32px;
    border: 1px solid white;
  }
  .hero {
    background-color: green !important;
    border-color: green;
  }
  .wall {
    background-image: url('../assets/walls.png');
  }
  /*.darkness {
    background-color: black !important;
    border-color: black !important;
  }*/
</style>
