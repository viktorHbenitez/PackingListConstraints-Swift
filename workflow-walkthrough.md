# Auto layout constraints

**Concept frame and bounds**  

A link:
[frame & bounds](https://es.stackoverflow.com/questions/44018/como-funciona-frame-position-y-bounds-en-el-layer-de-una-vista)

##  Animating dinamically created views
![imagen](../feature-animatingDynamicallyCreatedViews/assets/sketch5.gif)


### Steps

1. Create the image view programatically  
`let imageView = UIImageView(image: UIImage(named: "summericons_100px_0\(index).png"))` 

2. Create the constraints and active them
3. Adding additional dynamic animations

```swift

   // 1. Create the image
    let imageView = UIImageView(image: UIImage(named: "summericons_100px_0\(index).png"))
    imageView.backgroundColor = UIColor(red: 0.0, green: 0.0, blue: 0.0, alpha: 0.5)
    imageView.layer.cornerRadius = 5.0
    imageView.layer.masksToBounds = true
    imageView.translatesAutoresizingMaskIntoConstraints = false
    view.addSubview(imageView)
    
    // 2. Create constraints to the original image
    let conX = imageView.centerXAnchor.constraint(equalTo:view.centerXAnchor)
    let conBottom = imageView.bottomAnchor.constraint(equalTo:view.bottomAnchor, constant: imageView.frame.height)
    let conWidth = imageView.widthAnchor.constraint(equalTo:view.widthAnchor, multiplier: 0.33, constant: -50.0)
    let conHeight = imageView.heightAnchor.constraint(equalTo:imageView.widthAnchor)
    
    NSLayoutConstraint.activate([conX, conBottom, conWidth, conHeight])
    
    // 3. Animate and change constraints
    UIView.animate(withDuration: 0.8, delay: 0.0,
                   usingSpringWithDamping:  0.4, initialSpringVelocity: 0.0,
                   animations: {
                    conBottom.constant = -imageView.frame.size.height/2
                    conWidth.constant = 0.0  // return to the original size
                    self.view.layoutIfNeeded()
    },completion: nil)
  
```
