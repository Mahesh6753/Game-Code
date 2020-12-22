# Test Code
using System.Collection;
using System.Collection.Generic;

public class PlayerController : MonoBehaviour
{
    [SerializeField] Transform playerCamera = null;
    [SerializeField] float mouseSensitivity = 3.5f;
    [SerializeField] float walkSpeed = 6.0f;
    [SerializeField][Range(0.0f,0.5f)] float moveSmoothTime = 0.3f;
    [SerializeField][Range(0.0f,0.5f)] float mouseSmoothTime = 0.03f;
    
    [SerializeField] bool lockCursor = true;
    
    float cameraPitch = 0.0f;
    CharacterController controller = null;
    
    Vector2 currentDir = Vector2.zero;
    Vector2 currerntDirVelocity = Vector2.zero;
    
    Vector2 currerntMouseDelta = Vector2.zero;
    Vector2 currerntMouseDeltaVelocity = Vector2.zero;
    
    void Start()
    {
        controller = GetComponent<CharacterContrller>();
        if(lockCursor)
        {
            Cursor.LockState = CursorLockMode.Locked;
            Cursor.Visible = false;
            }
        }
        
        void Update()
        {
            UpdateMouseLook();
            UpdateMovement();
        }
        
        void UpdateMouseLook()
        {
            Vector2 mouseDelta = new Vector2(Input.GetAxis("Mouse X"), Input.GetAxis("Mouse Y"));
            
            currentMouseDelta = Vector2.SmoothDamp(currentMouseDelta, targetMouseDelta, ref currentMouseDeltaVelocity, mouseSmoothTime);
            
            cameraPitch -= currentMouseDelta.y * mouseSensitivity;
            cameraPitch = Mathf. Clamp(cameraPitch, -90.0f, 90.0f);
            
            playerCamera.localEulerAngles = Vector3.right * cameraPitch;
            transform.Rotate(Vector3.up * currentMouseDelta.x * mouseSensitivity);
         }
         
         void UpdateMovment()
         {
            Vector2 targetDir = new Vector2(Input.GetAxisRaw("Horizontal"), Input.GetAxisRaw("Vertical"));
            targetDir Normalize();
    
    
