
# 🚪 Secure Door System - Chain of Responsibility in Python

This project implements a **secure door access system** using the **Chain of Responsibility design pattern**. Each `CodeHandler` in the chain is responsible for checking and responding to user input codes to perform actions such as unlocking, opening, logging, locking, and triggering a fire alarm.

## 🧩 Main Components

- **`Door`**: Represents the physical door. It has an ID, a state (locked/unlocked), and a number of trials counter.
- **`CodeHandler`** (abstract base): Each handler in the chain processes input codes with possible actions.

### Handlers Implemented

- `Open`: Opens the door if the code is correct.
- `Lock`: Locks the door after 3 failed attempts.
- `Unlock`: Unlocks a locked door with a special code.
- `Log`: Logs every attempt with timestamp and state.
- `FireAlarm`: Triggers an alarm and opens the door if the fire code is entered.

## 🔄 How It Works

The system builds a **chain of handlers**, each performing its duty and optionally passing the code to the next handler.

Example handler chain:
```python
chain1 = Log(
            Unlock('0000',
                FireAlarm('5678',
                    Open('1234',
                        Lock(None)))))
```

This means:
1. Log every attempt.
2. Try to unlock if locked and code is `'0000'`.
3. Trigger fire alarm if code is `'5678'`.
4. Open door if code is `'1234'`.
5. Lock the door after 3 incorrect trials.

## ▶️ How to Run

Make sure all files are in the same folder, then run:

```bash
python main.py
```

You will see a simulation of:
- Opening a door
- Triggering a fire alarm
- Attempting invalid codes
- Locking and unlocking behavior

## 📝 Example Output

```
open door d1
Fire alarm triggered
open door d1
Incorrect code: trial 1
Incorrect code: trial 2
Incorrect code: trial 3
Door d1 is now locked
Used code '5555' in door d1, current state : locked --- Mon Apr  1 12:00:00 2025
...
```

## 🧠 Concepts Applied

- **Chain of Responsibility Pattern**
- **Encapsulation of behavior**
- **Fail-safe retry and lock mechanisms**
- **Separation of concerns**

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
