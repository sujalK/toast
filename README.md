# Toast Notification

This is a simple toast notification component that can come handy when
showing up the messages on certain events / actions.

## Steps to run the project
> The commands below can help to set up the project.

### This component is built using Vue ( Options API ), 
   ######  To get Started all you have to do is:

1. Install Project Dependencies
    > `npm install`

2. Launch the project
    > `npm run dev`

# Example Usage
1. Inside a component, we can import Toast component, then
   register it globally, after that, we can pass
   "type", and "show" props

   ```
     <toast
        type="success"
        :show="showToast"
        @hide="hide" 
      />
   ```
   
2. The value of `type` props can be:
   - success
   - warning
   - error

3. Optionally, there is an option to pass
   the message using `message` props
   
   *message appears on the toast notification*
   ```
     <toast
        type="success"
        message="The data saved successfully"
        :show="showToast"
        @hide="hide" 
      />
   ```
   