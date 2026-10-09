//ATTACH THIS A GAME CHARACTER GameObject.Good for  Rougelike puzzle games, tactics games.
//The character snaps to whole tile position rather than moving continuously.

//CODE PROPER

using UnityEngine;

public class GridMovement: MonoBehaviour
{
    public float tileSize = 1.0f; //size of one grid cell
    public float moveSpeed = 10f; //how fast we glide between tikes (feel not logic)\

    private Vector3 targetPosition;
    private bool is Moving = false;

    void Start()
    {
        //Snap Position to the grid so everything lines up
        targetPosition = SnapToGrid(transform.position);
        transform.position = targetPosition;
    }
    void Update()
    {
        if (!isMoving)
        {
            HandleInput();
        }
        else
        {
            //smoothly glide to the next tile (this will be your presentation, not the actual logic)
            if (Vector3.Distance(transform.position, targetPosition)< 0.001f)
            {
                transform.position = targetPosition;
                isMoving = false;
            }
        }
    }
    void HandleInput()
    {
        Vector3 direction = Vector.zero;
        if(Input.GetKeyDown(KeyCode. W)) direction = Vector3.up;
        else if Input.GetKeyDown(KeyCode. S)) direction = Vector3.down;
        else if Input.GetKeyDown(KeyCode. A)) direction = Vector3.left;
        else if Input.GetKeyDown(KeyCode. D)) direction = Vector3.right;

        if(direction != Vector3.zero)
        {
            targetPosition = transform.position + direction * tileSize;
            isMoving = true;
        }
    }
    Vector3 SnapToGrid(Vector3 pos)
    {
        return new  Vector3(
            Mathf.Round(pos.x / tileSize) * tileSize,
            Mathf.Round(pos.y / tileSize) * tileSize,
            pos.z
        );
    }
}

//FREE (VECTOR BASED MOVEMENT)
//ATTACH THIS TO A CHARACTER GameObject. GOOD FOR TOP-DOWN ACTION GAMES, PLATFORMERS
//(HORIZONTAL AXIS), twin-stick shooters. Movement is continuous, not tile locked

using UnityEngine;

public class FreeMovement : MonoBehaviour
{
    public float moveSpeeed = 5f;

    void Update()
    {
        //GetAxis gices smooth values between -1 and 1 (supports keyboard and controller)
        float horizontal = Input.GetAxis("Horizontal"); //A/D or Left/Right Arrows
        float vertical = Input.GetAxis("Vertical"); //W/S or up/down arrows

        Vector3 direction = new Vector(horizontal, vertical, 0f);
        //normalize so diagonal movement isn't faster than straight movement
        if(direction.magnitude.1f)
        {
            direction.Normalize();
        }
        transform.position += direction * moveSpeed * Time.deltaTime
    }
}


//PHYSICS-BASED MOVEMENT
//attach this to character GameObject  that also has RigidBody2D component
//(component > Physics 2D > RigidBody 2D). Good for platformers with momentum, vehicle, anything that should feels like it has mass, gravity, and friction

using UnityEngine;
[RequireComponent(typeof(RigidBody2D))]

public class PhysicsMovement :  MovementBehaviour
{
    public float moveForce = 10f;
    public float jumpForce = 7f;
    public float maxSpeed = 6f;

    private RigidBody2D rb;
    private bool isGrounded = false;

    void Start()
    {
        rb = GetComponent<RigidBody2D>()
    }
    void Update()
    {
        //read input in Update (input should always be checked every frame)
        if(Input.GetKeyDown(KeyCode.Space) && isGrounded)
        {
            rb.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
        }
    }
        void FixedUpdate()
        {
        //physics changes belong in FixedUpdate, which runs on  a fixed timestep
        //independent of frame rate - keep physics simulation stable
        float horizontal = Input.GetAxis("Horizontal");
        rb.Addforce(new Vector2(horizontal * moveForce, 0f));

        //clamp horizontal speed so the character doesn't accelerate forever

        if(Mathf.Abs(rb.velocity.x)>maxSpeed)
        {
            rb.velocity = newVector2(Mathf.Sign(rb.velocity.x)) * maxSpeed, rb.velocity.y
        }
    }
    void OnCollisionEnter2D(Collision2D collision)
    {
        if(collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = true;
        }
    }
    void OnCollisionExit2D(Collision2D collision)
    {
        if(collision.gameObject.CompareTag("Ground"))
        {
            isGrounded = false;
            
        }
    }
}
