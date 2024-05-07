# Pong
import UIKit

class ViewController: UIViewController {
    
    var ball = UIView()
    var paddle = UIView()
    var timer: Timer?
    var ballVelocity = CGPoint(x: 5, y: 5)
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        ball = UIView(frame: CGRect(x: view.frame.width/2 - 15, y: view.frame.height/2 - 15, width: 30, height: 30))
        ball.backgroundColor = UIColor.red
        ball.layer.cornerRadius = 15
        view.addSubview(ball)
        
        paddle = UIView(frame: CGRect(x: view.frame.width/2 - 50, y: view.frame.height - 50, width: 100, height: 10))
        paddle.backgroundColor = UIColor.blue
        view.addSubview(paddle)
        
        timer = Timer.scheduledTimer(timeInterval: 0.05, target: self, selector: #selector(update), userInfo: nil, repeats: true)
    }
    
    @objc func update() {
        ball.center.x += ballVelocity.x
        ball.center.y += ballVelocity.y
        
        if ball.frame.intersects(paddle.frame) {
            ballVelocity.y *= -1
        }
        
        if ball.frame.origin.x <= 0 || ball.frame.origin.x + ball.frame.width >= view.frame.width {
            ballVelocity.x *= -1
        }
        
        if ball.frame.origin.y <= 0 || ball.frame.origin.y + ball.frame.height >= view.frame.height {
            ballVelocity.y *= -1
        }
    }
    
    override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {
        if let touch = touches.first {
            let touchLocation = touch.location(in: view)
            paddle.center.x = touchLocation.x
        }
    }
}
