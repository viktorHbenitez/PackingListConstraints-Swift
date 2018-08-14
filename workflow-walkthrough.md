# Auto layout constraints
![imagen](../feature-animationBy-ReplacinConstraints/assets/tutorial1.png)

##  Animating by replacing constraints

If you want to modify the multiplier, or change a constraint in any other way, you’ll need to remove the constraint then add a new one in its place.  

Change the  `CenterX`  TItleLable  
![imagen](../feature-animationBy-ReplacinConstraints/assets/sketch3.gif)  

### Steps

1. Assing an identifier to `CenterY`  constraint 

2. Print all constraints
```swift

    titleLabel.superview?.constraints.forEach { constraint in
            print("\(constraint.description)") // 1. Show all the constraints

            
<NSLayoutConstraint:0x6040002927f0 UIView:0x7fa584f193b0.height == 66   (active)>
<NSLayoutConstraint:0x604000291e40 UILabel:0x7fa584f195a0'Packing List'.centerY == UIView:0x7fa584f193b0.centerY + 10   (active)>
<NSLayoutConstraint:0x60400028cc10 UILabel:0x7fa584f195a0'Packing List'.centerX == UIView:0x7fa584f193b0.centerX   (active)>
<NSLayoutConstraint:0x604000289ec0 H:[UIButton:0x7fa584c2cdb0'+']-(8)-|   (active, names: '|':UIView:0x7fa584f193b0 )>
<NSLayoutConstraint:0x604000284830 UIButton:0x7fa584c2cdb0'+'.centerY == UILabel:0x7fa584f195a0'Packing List'.centerY   (active)>
```
2. Search the specific constraint  in foreach loop
3. Change the constraint: Delete the  CenterY and create other again (because we want to modify the multiplier)

```swift 
 
        if constraint.identifier == "TitleCenterY"{  // 2 search the constraint with identifier
            constraint.isActive = false  // 3. Delete the constraint
            
            // Adding constraints programmatically to change multiplier atribute
            
            /* 3. CREATE THE CONSTRAINT */
            // equation : Title.CenterY = Menu.CenterY * 0.67 + 0.0
            let newConstraint = NSLayoutConstraint(item: titleLabel,
                                                   attribute: .centerY,
                                                   relatedBy: .equal,
                                                   toItem: titleLabel.superview!,
                                                   attribute: .centerY,
                                                   multiplier: isMenuOpen ? 0.67 : 1.0,
                                                   constant: 10.0)
            
            newConstraint.identifier = "TitleCenterY"  // Add identifier
            newConstraint.isActive = true // Active the new constraint
            
            return
        }
```
**Description the elements of the new constraint**  
The parameters are as follows:
• `item`: The first item in the equation; in this case, the title label.
• `attribute`: The attribute of the first item of the new constraint.
• `relatedBy`: A constraint can represent either a mathematical equality or an inequality. In this book, you’ll only use equality expressions, so here you use .equal to represent this relationship.
• `toItem`: The second item in the constraint equation; in this case, it’s your title’s superview.
• `attribute`: The attribute of the second item of the new constraint.
• `multiplier`: The equation multiplier as discussed earlier.
• `constant`: The equation constant.

4. Update with animation  

```swift
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



