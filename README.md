/**
 * extractDataFromWebsite
 *
 * This function extracts data from a given website.
 *
 * @param {string} url - The URL of the website to extract data from.
 * @param {string} selector - The CSS selector for the elements to extract data from.
 *
 * @returns {array} An array of objects containing the extracted data.
 */
const extractDataFromWebsite = (url, selector) => {
  // Validate parameters
  if (!url || !selector) {
    throw new Error('Missing parameter(s).');
  }

  // Fetch the website
  let response;
  try {
    response = await fetch(url);
  } catch (err) {
    console.error(`Error fetching website: ${err}`);
    return [];
  }

  // Parse the response
  let html;
  try {
    html = await response.text();
  } catch (err) {
    console.error(`Error parsing response: ${err}`);
    return [];
  }

  // Extract the data
  let extractedData = [];
  try {
    const elements = document.querySelectorAll(selector);
    elements.forEach(element => {
      extractedData.push({
        text: element.innerText,
        html: element.innerHTML
      });
    });
  } catch (err) {
    console.error(`Error extracting data: ${err}`);
    return [];
  }

  return extractedData;
};
