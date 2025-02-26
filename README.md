import React from 'react'
import { useState } from "react";
// import axios from 'axios'

const Form = () => {
    const [startTime, setStartTime] = useState("10:00");
    const [endTime, setEndTime] = useState("10:30");
    const [isOpen, setIsOpen] = useState(false);
    const [difference, setDifference] = useState(null);

    const toggleDropdown = () => {
        setIsOpen(!isOpen);
    };

    const calculateDifference = () => {
        if (!startTime || !endTime) {
            console.log("Please select both start and end times.");
            return;
        }

        const start = new Date(`2000-01-01T${startTime}`);
        const end = new Date(`2000-01-01T${endTime}`);

        let diffInHours = (end - start) / (1000 * 60 * 60); // Convert milliseconds to hours

        if (diffInHours < 0) {
            diffInHours += 24; // Handles cases where endTime is past midnight
        }

        diffInHours = diffInHours.toFixed(2); // Round to 2 decimal places
        setDifference(diffInHours);

        // ✅ Log the results in the console
        console.log(`Start Time: ${startTime}`);
        console.log(`End Time: ${endTime}`);
        console.log(`Time Difference: ${diffInHours} hours`);
    };

    const onSumbitHandler = async (event) => {
        event.preventDefault()
    
        try {
        
            const {data} = await axios.post(backendUrl + '/api/user/login', {password, email,})
            if (data.success) {
console.log(success.message)
            } else {
            //   toast.error(data.message)
            console.log(errror.message)
            }
            
          
        } catch (error) {
        //   toast.error(error.message)
        console.log(error.message)
        }
    
      }

    return (

        <form onSubmit={onSumbitHandler} className='min-h-[80vh] flex items-center'>

        <div>
            <div className="flex">
                <input type="checkbox" id='checkbox' className="h-4 w-6 mt-0.5 border-gray-200 rounded-lg text-blue-600 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none" />
                <label for="hs-default-checkbox" className="text-sm text-gray-500 ms-3 dark:text-neutral-400">Default checkbox</label>
            </div>
            <div style={{ display: "flex", gap: "10px", flexDirection: "column" }}>
                <label>
                    Start Time:
                    <input
                        type="time"
                        value={startTime}
                        onChange={(e) => setStartTime(e.target.value)}
                    />
                </label>

                <label>
                    End Time:
                    <input
                        type="time"
                        value={endTime}
                        onChange={(e) => setEndTime(e.target.value)}
                    />
                </label>

                <button onClick={calculateDifference} style={{ padding: "5px", cursor: "pointer" }}>
                Calculate Difference
            </button>

            {difference !== null && <p>Time Difference: {difference} hours</p>}
            </div>

{/* center elements */}
            {/* <div className="min-h-screen flex items-center justify-center bg-gray-100">
            <Dropdown />
        </div> */}
         
            <div className="relative inline-block text-left">
            {/* Green-colored text above the dropdown */}
            <p className="text-green-500 mb-2">GeeksForGeeks</p>

            <div>
                <button
                    onClick={toggleDropdown}
                    className="inline-flex justify-center w-full rounded-md 
                    border border-gray-300 shadow-sm px-4 py-2 bg-white 
                    text-sm font-medium text-gray-700 hover:bg-gray-50 
                    focus:outline-none"
                >
                    Options
                    <svg
                        className="ml-2 -mr-1 h-5 w-5"
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                        aria-hidden="true"
                    >
                        <path
                            strokeLinecap="round"
                            strokeLinejoin="round"
                            strokeWidth="2"
                            d="M19 9l-7 7-7-7"
                        />
                    </svg>
                </button>
            </div>

            {isOpen && (
                <div
                    className="origin-top-right absolute right-0 mt-2 w-56 
                    rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5
                    focus:outline-none"
                    role="menu"
                >
                    <div className="py-1" role="none">
                        <a
                            href="#"
                            className="block px-4 py-2 text-sm text-gray-700 
                            hover:bg-gray-100"
                            role="menuitem"
                        >
                            Account settings
                        </a>
                        <a
                            href="#"
                            className="block px-4 py-2 text-sm text-gray-700
                            hover:bg-gray-100"
                            role="menuitem"
                        >
                            Support
                        </a>
                        <a
                            href="#"
                            className="block px-4 py-2 text-sm text-gray-700
                            hover:bg-gray-100"
                            role="menuitem"
                        >
                            License
                        </a>
                    </div>
                </div>
            )}
        </div>
        <button type='submit' className='bg-blue-500 text-white w-full py-2 rounded-md text-base'>Create Account</button>
        </div>      
    </form>
    )
}

const styles = {
    inputWrapper: {
        position: "relative",
        padding: "10px",
        border: "1px solid #ccc",
        borderRadius: "5px",
        cursor: "pointer",
        textAlign: "center",
        background: "#f9f9f9",
        width: "180px",
        fontSize: "16px",
        color: "#333",
    },
    hiddenInput: {
        position: "absolute",
        opacity: 0,
        width: "100%",
        height: "100%",
        cursor: "pointer",
    },
};

export default Form
