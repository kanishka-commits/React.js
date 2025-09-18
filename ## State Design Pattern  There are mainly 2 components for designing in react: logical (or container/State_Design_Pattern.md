## State Design Pattern

There are mainly 2 components for designing in react: logical (or container/smart) and presentational (or dumb) components.\
These design pattern focused on separating concerns, aiming for cleaner, more maintainable, and reusable code.\

We can divide components by 1st defining: Props, States and Events\

Let's take example of Lottery Ticket Generator:
1. Build lowest component i.e. TicketNumber
2. TicketNumber contains:
   - zero props as they don't have any child components
   - zero states as there is no logic
   - zero events
3. Ticket contains:
   - 1 prop, i.e. ticket number, received from Lottery component
   - zero state as there is no logic
   - zero events
4. Lottery contains:
   - zero props as no prop is received from App component OR app can tell **winning sum** as well as **number of lottery tickets**
   - 1 state to store the ticket
   - 1 event, to create a button which generates ticket
   
   
