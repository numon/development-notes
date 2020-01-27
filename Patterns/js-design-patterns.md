# Factory

Example: 

```javascript
class WoodenDoor {
  constructor(width, height){
    this.width = width
    this.height = height
  }

  getWidth(){
    return this.width
  }

  getHeight(){
    return this.height
  }
}
```

Creating factory for Door
```javascript
const DoorFactory = {
  makeDoor : (width, height) => new WoodenDoor(width, height)
}
```

Use:
```javascript
const door = DoorFactory.makeDoor(100, 200)
console.log('Width:', door.getWidth())
console.log('Height:', door.getHeight())
```

# Factory Method
