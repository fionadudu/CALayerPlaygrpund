# CALayerPlaygrpund

每一个view都有一个layer. layer比view更广泛，和动画。所以对层进行装饰，更能实现动画效果，同时能让效果更加的明显和吸引人。
当然，不同的效果需要不用的方法和功能。

### 举个本例子中的简单代码：

import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var viewForLayer: UIView!
    
    var  l : CALayer {
    return viewForLayer.layer
    }
    override func viewDidLoad() {
        super.viewDidLoad()
        setUpLayer()
    }
    
    func setUpLayer(){
        l.backgroundColor = UIColor.blueColor().CGColor
        l.borderWidth = 100.0
        l.borderColor = UIColor.redColor().CGColor
        l.shadowOpacity = 0.7
        l.shadowRadius = 10.0
        l.contents = UIImage(named: "star")?.CGImage
        l.contentsGravity = kCAGravityCenter
    }

    @IBAction func tapGestureRecognized(sender: UITapGestureRecognizer) {
        l.shadowOpacity = l.shadowOpacity == 0.7 ? 0.0 : 0.7
    }
    @IBAction func pinchGestureRecognized(sender: UIPinchGestureRecognizer) {
        let offset: CGFloat = sender.scale < 1 ? 5.0 : -5.0
        let oldFrame = l.frame
        let oldOrigin = oldFrame.origin
        let newOrigin = CGPoint(x: oldOrigin.x + offset, y: oldOrigin.y + offset)
        let newSize = CGSize(width: oldFrame.width + (offset * -2.0), height: oldFrame.height + (offset * -2.0))
        let newFrame = CGRect(origin: newOrigin, size: newSize)
        if newFrame.width >= 100.0 && newFrame.width <= 300.0 {
            l.borderWidth -= offset
            l.cornerRadius += (offset / 2.0)
            l.frame = newFrame
        }
    }
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }


}
