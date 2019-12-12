# UISegmentedControl_ProgrammaticView

- A UISegmentedControl is a subclass of UIControl. 
- Constrols are responsible for calling methods on their target in response to some event.

![Screen Shot 2019-12-11 at 20 49 16](https://user-images.githubusercontent.com/24994818/70678451-bf927380-1c57-11ea-964d-06ebef2f5554.png)

``` swift
//
//  ViewController.swift
//  MapApp
//
//  Created by Carlos Santiago Cruz on 11/12/19.
//  Copyright © 2019 Carlos Santiago Cruz. All rights reserved.
//

import UIKit
import MapKit

class ViewController: UIViewController {
    
    var mapView: MKMapView!

    override func loadView() {
        // first, remove the Main storyboard, to override that view.
        mapView = MKMapView()
        view = mapView
        
        // create a segmentedcontrol View
        // which is inherence from UIControl, but this UIControl inherentance from UIView
        let segmentedControl = UISegmentedControl(items: ["standard", "Hybrid", "Satellite"])
        segmentedControl.backgroundColor = UIColor.white.withAlphaComponent(0.5)
        segmentedControl.selectedSegmentIndex = 0
        
        segmentedControl.addTarget(self, action: #selector(self.mapTypeChanged(_:)), for: .valueChanged)
        
        segmentedControl.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(segmentedControl)
        
        // create them again
        let topConstraint = segmentedControl.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 8)
        let leadingConstraint = segmentedControl.leadingAnchor.constraint(equalTo: view.layoutMarginsGuide.leadingAnchor)
        let trailingConstraint = segmentedControl.trailingAnchor.constraint(equalTo: view.layoutMarginsGuide.trailingAnchor)
        
        topConstraint.isActive = true
        leadingConstraint.isActive = true
        trailingConstraint.isActive = true
    }
    
    @objc func mapTypeChanged(_ segmentedControl: UISegmentedControl)
    {
        switch segmentedControl.selectedSegmentIndex {
        case 0:
            mapView.mapType = .standard
        case 1:
            mapView.mapType = .hybrid
        case 2:
            mapView.mapType = .satellite
        default:
            break
        }
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        print("MapViewController loaded its view")
    }
}
```
