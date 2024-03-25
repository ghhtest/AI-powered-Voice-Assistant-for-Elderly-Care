# AI-powered-Voice-Assistant-for-Elderly-Care
Entwickeln Sie einen KI-gesteuerten Sprachassistenten, der älteren Menschen hilft, sich mit ihren Lieben zu verbinden, Termine zu verwalten und im Notfall Hilfe zu rufen.
import datetime

# Simulating a database for contacts and appointments
contacts = {"doctor": "Dr. Smith", "family": "John Doe", "emergency": "112"}
appointments = []

def add_appointment(date_time, description):
    appointments.append({"date": date_time, "description": description})
    return "Appointment added successfully."

def view_appointments():
    if not appointments:
        return "No appointments found."
    response = "Your appointments:\n"
    for appointment in appointments:
        response += f"- {appointment['date']} for {appointment['description']}\n"
    return response

def call_for_help():
    # Simulate sending a message to an emergency contact
    emergency_contact = contacts['emergency']
    return f"Help called, contacting {emergency_contact}."

def connect_with_loved_one():
    # Simulate connecting with a family member
    family_contact = contacts['family']
    return f"Connecting you with {family_contact}."

def handle_command(command):
    if command.startswith("add appointment"):
        # Expecting command format: "add appointment YYYY-MM-DD HH:MM Description"
        parts = command.split(" ", 3)
        if len(parts) < 4:
            return "Invalid command format for adding an appointment."
        try:
            date_time = datetime.datetime.strptime(parts[1] + " " + parts[2], "%Y-%m-%d %H:%M")
            return add_appointment(date_time, parts[3])
        except ValueError:
            return "Invalid date format."
    elif command == "view appointments":
        return view_appointments()
    elif command == "call for help":
        return call_for_help()
    elif command == "connect with loved one":
        return connect_with_loved_one()
    else:
        return "Command not recognized."

# Demo interaction
if __name__ == "__main__":
    while True:
        command = input("How can I assist you? (type 'exit' to stop) ")
        if command.lower() == 'exit':
            break
        response = handle_command(command)
        print(response)
