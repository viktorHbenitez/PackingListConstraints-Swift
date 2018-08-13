# Auto layout constraints
##  Animating UILabel constraints

Loop over the list of constraints affecting the menu bar view, but this time you are looking for a certain constraint to adjust.  

Change the  `CenterX`  TItleLable  
![imagen](../master/assets/sketch2.gif)  

### Steps

1. Print all constraints  
```swift
<NSLayoutConstraint:0x6040002927f0 UIView:0x7fa584f193b0.height == 66   (active)>
<NSLayoutConstraint:0x604000291e40 UILabel:0x7fa584f195a0'Packing List'.centerY == UIView:0x7fa584f193b0.centerY + 10   (active)>
<NSLayoutConstraint:0x60400028cc10 UILabel:0x7fa584f195a0'Packing List'.centerX == UIView:0x7fa584f193b0.centerX   (active)>
<NSLayoutConstraint:0x604000289ec0 H:[UIButton:0x7fa584c2cdb0'+']-(8)-|   (active, names: '|':UIView:0x7fa584f193b0 )>
<NSLayoutConstraint:0x604000284830 UIButton:0x7fa584c2cdb0'+'.centerY == UILabel:0x7fa584f195a0'Packing List'.centerY   (active)>
```
2. Search the specific constraint  
3. Change the constraint  
4. Update with animation  



```swift

 titleLabel.superview?.constraints.forEach { constraint in
        print("\(constraint.description)") // 1. Show all the constraints

        // UILabel:0x7ff50643ceb0'Packing List'.centerX == UIView:0x7ff50643ccc0.centerX - 150
        if constraint.firstItem === titleLabel && constraint.firstAttribute == .centerX { // 2. search the const with the format
            constraint.constant = isMenuOpen ? -130.0 : 0.0  // 3. Change the specific constraint
            return
        }
        
 }
    
    // titleLabel.text = isMenuOpen ? "Select item" : "Packing List"
    // menuHeightConstraints.constant = isMenuOpen ? 200.0 : 60.0  // IBoutlet height
    
    // ANIMATION THE CONSTRAINT
    UIView.animate(withDuration: 1.0, delay: 0.0,
                   usingSpringWithDamping: 0.4, initialSpringVelocity: 10.0,
                   options: .curveEaseIn,
                   animations: {
                    self.view.layoutIfNeeded()  // 4 Important update constraints wiht animation
                    
                    // Rotation + when the menu expand
                    // let angle: CGFloat = self.isMenuOpen ? .pi / 4 : 0.0
                    // self.buttonMenu.transform = CGAffineTransform(rotationAngle: angle)
    },completion: nil)
 
```



