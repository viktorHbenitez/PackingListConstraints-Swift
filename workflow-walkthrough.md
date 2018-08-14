# Auto layout constraints
![imagen](../feature-animationBy-ReplacinConstraints/assets/tutorial1.png)

##  Adding Menu Content

you create a new instance of HorizontalItemList in slider to hold your new items, assign a closure expression to didSelectItem and then finally add slider to the menu bar.  
![imagen](../master/assets/sketch4.gif)  

### Steps

1. Add Menu content instance  `var slider: HorizontalItemList!` 

2. in HorizontalItemList call the block (declarate, invoke and definition)
```swift

  var didSelectItem: ((_ index: Int)->())?  // 1. declarate
 
  @objc func didTapImage(_ tap: UITapGestureRecognizer) {
    didSelectItem?(tap.view!.tag) // 2. Invoke
  }
  
  
  // **** ADDING MENU CONTENT
    if isMenuOpen {
        slider = HorizontalItemList(inView: view)  // Add the component in the view
      
      slider.didSelectItem = {index in  // 2. Definition
            print("add \(index)")
            self.items.append(index)  // 2. append index of position image (int)
            self.tableView.reloadData()
            
            self.actionToggleMenu(self)  // 3. hide the menu again, call the function
        }
        self.titleLabel.superview!.addSubview(slider)
        
    } else {
        slider.removeFromSuperview()
    }
  }
  
```
2. Get the index of the image selected and append in the array of position
3. Reload the data with the delegate methods
```swift

  // **** ADDING MENU CONTENT
    if isMenuOpen {
        slider = HorizontalItemList(inView: view)  // Add the component in the view
      
      slider.didSelectItem = {index in 
            print("add \(index)")
            self.items.append(index)  // 2. append index of position image (int)
            self.tableView.reloadData()  // Reload the TableView and update with the cellForRowAt 
            
            self.actionToggleMenu(self)  // hide the menu again, call the function
        }
        self.titleLabel.superview!.addSubview(slider)
        
    } else {
        slider.removeFromSuperview()
    }
  }
  
  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {}

  
```
