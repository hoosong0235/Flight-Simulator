# Phase 4. Implementation

## 1. Implement PC Control

Q: Accelerate Blade Rotation
E: Deaccelerate Blade Rotation
W: Accelerate Helicopter Vertical Speed Forward
A: Accelerate Helicopter Horizontal toward Left
S: Accelerate Helicopter Vertical Speed Backward
D: Accelerate Helicopter Horizontal toward Right

    if (Input.GetKey(KeyCode.Q)) {
        MainRotorSpeed = Mathf.Min(30f, MainRotorSpeed + (1f * Time.deltaTime));
    }
    if (Input.GetKey(KeyCode.E)) {
        MainRotorSpeed = Mathf.Max(0f, MainRotorSpeed - (1f * Time.deltaTime));
    }
    if (Input.GetKey(KeyCode.W)) {
        WSSpeed = Mathf.Min(3f, WSSpeed + (1f * Time.deltaTime));
    }
    if (Input.GetKey(KeyCode.A)) {
        ADSpeed = Mathf.Max(-3f, ADSpeed - (1f * Time.deltaTime));
    }
    if (Input.GetKey(KeyCode.S)) {
        WSSpeed = Mathf.Max(-3f, WSSpeed - (1f * Time.deltaTime));
    }
    if (Input.GetKey(KeyCode.D)) {
        ADSpeed = Mathf.Min(3f, ADSpeed + (1f * Time.deltaTime));
    }

## 2. Implement Set Blade Rotation

    target = GameObject.Find("Blade");

    target.transform.rotation = new Vector3(
        target.transform.rotation.x,
        target.transform.rotation.y,
        target.transform.rotation.z + MainRotorSpeed,
    );

## 3. Implement Set Helicopter Location

    target = GameObject.Find("Helicopter");

    target.transform.position = new Vector3(
        target.transform.position.x,
        target.transform.position.y,
        target.transform.position.z + (1000f * (MainRotorSpeed - 15f) * Time.deltaTime),
    );

    if (isFlying) {
        target.transform.position = new Vector3(
            target.transform.position.x + (1000f * ADSpeed * Time.deltaTime),
            target.transform.position.y + (1000f * WSSpeed * Time.deltaTime),
            target.transform.position.z,
        )
    };

## 4. Implement Set Helicopter Rotation

    target = GameObject.Find("Helicopter");

    target.transform.rotation = new Vector3(
        10 * WSSpeed,
        10 * ADSpeed,
        target.transform.rotation.z,
    );

## 5. Implement 3rd Person View

    target = GameObject.Find("player");
    origin = GameObject.Find("Helicopter");

    target.transform.position = new Vector3(
        origin.transform.position.x,
        origin.transform.position.y - 2000f,
        origin.transform.position.z + 1000f,
    );

# Phase 7. Enhance Control

## 1. Enhance PC Control

Q: Accelerate Blade Rotation
E: Deaccelerate Blade Rotation
W: Accelerate Vertical Speed Forward
A: Accelerate Horizontal toward Left
S: Accelerate Vertical Speed Backward
D: Accelerate Horizontal toward Right
**Tab: Switch Person View**

    if (Input.GetKeyDown(Tab)) {
        isThirdPerson = !isThirdPerson;
    }

## 2. Implement VR Control

L2: Switch Person View
R2: Switch Person View
Left Joystick: Accelerate or Deaccelerate Blade Rotation
Right Joystick: Accelerate Helicopter Speed

## 3. Enhance Set Helicopter Location

    target = GameObject.Find("Helicopter");

    target.transform.position = new Vector3(
        target.transform.position.x,
        target.transform.position.y,
        target.transform.position.z + (1000f * (MainRotorSpeed - 15f) * Time.deltaTime),
    );

    if (isFlying) {
        target.transform.position = new Vector3(
            target.transform.position.x + (1000f * ADSpeed * Time.deltaTime),
            target.transform.position.y + (1000f * WSSpeed * Time.deltaTime),
            target.transform.position.z,
        )
    };

    zvalue += 10f * ADSpeed * Time.deltaTime;

## 4. Enhance Set Helicopter Rotation

    target = GameObject.Find("Helicopter");

    target.transform.rotation = new Vector3(
        10 * WSSpeed,
        10 * ADSpeed,
        zValue,
    );

## 5. Enhance 3rd Person View

    target = GameObject.Find("player");
    origin = GameObject.Find("Helicopter");

    target.transform.position = new Vector3(
        origin.transform.position.x + (2000f * Mahtf.Sin(Mathf.Deg2Rad(zValue))),
        origin.transform.position.y - (2000f * Mathf.Cos(Mathf.Deg2Rad(zValue))),
        origin.transform.position.z + 1000f,
    );

## 6. Implement 1st Person View

    target = GameObject.Find("player");
    origin = GameObject.Find("Seat");

    target.transform.position = origin.transform.position;
