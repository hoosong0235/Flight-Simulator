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
