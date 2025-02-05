using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public float speed = 5f;
    public float turnSpeed = 100f;

    void Update()
    {
        // Move player forward and backward
        float move = Input.GetAxis("Vertical") * speed * Time.deltaTime;
        transform.Translate(0, 0, move);

        // Rotate player left and right
        float turn = Input.GetAxis("Horizontal") * turnSpeed * Time.deltaTime;
        transform.Rotate(0, turn, 0);
    }
}
using Photon.Pun;

public class NetworkManager : MonoBehaviourPunCallbacks
{
    void Start()
    {
        PhotonNetwork.ConnectUsingSettings(); // Connect to Photon servers
    }

    public override void OnConnectedToMaster()
    {
        PhotonNetwork.JoinRandomRoom(); // Try to join a random room
    }

    public override void OnJoinRandomFailed(short returnCode, string message)
    {
        PhotonNetwork.CreateRoom(null, new Photon.Realtime.RoomOptions { MaxPlayers = 10 }); // Create a room if none exists
    }
}
using UnityEngine;

public class Gun : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform barrel;
    
    void Update()
    {
        if (Input.GetButtonDown("Fire1"))
        {
            Shoot();
        }
    }

    void Shoot()
    {
        Instantiate(bulletPrefab, barrel.position, barrel.rotation);
    }
}
