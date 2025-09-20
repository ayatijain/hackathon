# gdg-hackathon
import React, { useState } from 'react';
import { Bot, Factory, Truck, Package, Settings, DollarSign, Lightbulb, BarChart3, Leaf, Zap, Star, MessageCircle, Users, Building } from 'lucide-react';

const CustomerJourney = () => {
  const [selectedEnterprise, setSelectedEnterprise] = useState('manufacturing');
  const [selectedDepartment, setSelectedDepartment] = useState('Operations');
  const [currentSuggestion, setCurrentSuggestion] = useState('');
  const [activeTab, setActiveTab] = useState('suggestions');
  const [sustainabilityScore, setSustainabilityScore] = useState(0);
  const [inputs, setInputs] = useState({
    energy: '',
    waste: '',
    transport: '',
    water: '',
    employees: ''
  });
  const [reviews, setReviews] = useState([
    { name: "Raj Patel", company: "Mumbai Manufacturing", rating: 5, text: "Saved ₹3L annually with AI recommendations!" },
    { name: "Priya Singh", company: "Delhi Logistics", rating: 4, text: "Great insights for our fleet management." },
    { name: "Amit Kumar", company: "Bangalore Services", rating: 5, text: "The sustainability score helped us get green certification." }
  ]);
  const [newReview, setNewReview] = useState({ name: '', company: '', rating: 5, text: '' });

  const enterprises = {
    manufacturing: {
      name: "Manufacturing & Production",
      icon: <Factory className="w-6 h-6" />,
      departments: ["Operations", "Production", "Quality Control", "Assembly", "Packaging"]
    },
    logistics: {
      name: "Logistics & Transportation",
      icon: <Truck className="w-6 h-6" />,
      departments: ["Fleet Management", "Warehouse", "Route Planning", "Cargo Handling", "Distribution"]
    },
    retail: {
      name: "Retail & E-commerce",
      icon: <Package className="w-6 h-6" />,
      departments: ["Store Operations", "Inventory", "Customer Service", "Online Sales", "Procurement"]
    },
    services: {
      name: "Professional Services",
      icon: <Settings className="w-6 h-6" />,
      departments: ["Operations", "IT", "Office Management", "Client Relations", "Administration"]
    },
    textile: {
      name: "Textile & Garments",
      icon: <Factory className="w-6 h-6" />,
      departments: ["Weaving", "Dyeing", "Cutting", "Stitching", "Quality Check", "Finishing"]
    },
    food: {
      name: "Food & Beverage",
      icon: <Package className="w-6 h-6" />,
      departments: ["Processing", "Packaging", "Quality Control", "Storage", "Distribution"]
    },
    automotive: {
      name: "Automotive & Parts",
      icon: <Settings className="w-6 h-6" />,
      departments: ["Assembly", "Parts Manufacturing", "Quality Testing", "Paint Shop", "Final Assembly"]
    },
    chemicals: {
      name: "Chemicals & Pharmaceuticals",
      icon: <Factory className="w-6 h-6" />,
      departments: ["Production", "R&D", "Quality Control", "Safety", "Packaging"]
    },
    construction: {
      name: "Construction & Real Estate",
      icon: <Settings className="w-6 h-6" />,
      departments: ["Project Management", "Construction", "Materials", "Safety", "Design"]
    },
    agriculture: {
      name: "Agriculture & Agro-processing",
      icon: <Leaf className="w-6 h-6" />,
      departments: ["Farming", "Processing", "Storage", "Distribution", "Quality Control"]
    },
    electronics: {
      name: "Electronics & Technology",
      icon: <Zap className="w-6 h-6" />,
      departments: ["Assembly", "Testing", "R&D", "Quality Control", "Packaging"]
    },
    healthcare: {
      name: "Healthcare & Medical",
      icon: <Users className="w-6 h-6" />,
      departments: ["Patient Care", "Administration", "Equipment", "Pharmacy", "Laboratory"]
    },
    education: {
      name: "Education & Training",
      icon: <Users className="w-6 h-6" />,
      departments: ["Administration", "IT", "Facilities", "Student Services", "Library"]
    },
    hospitality: {
      name: "Hospitality & Tourism",
      icon: <Users className="w-6 h-6" />,
      departments: ["Front Office", "Housekeeping", "Food Service", "Maintenance", "Events"]
    },
    energy: {
      name: "Energy & Utilities",
      icon: <Zap className="w-6 h-6" />,
      departments: ["Generation", "Distribution", "Maintenance", "Customer Service", "Operations"]
    }
  };

  const suggestions = {
    manufacturing: {
      "Operations": "Implement energy-efficient machinery scheduling to reduce 15% power consumption and save ₹3L annually",
      "Production": "Switch to biodegradable packaging materials - save ₹2L annually in disposal costs",
      "Quality Control": "Digital quality checks reduce paper usage by 80% - save ₹50K annually",
      "Assembly": "Optimize assembly line workflow to reduce energy consumption by 20%",
      "Packaging": "Use eco-friendly packaging materials to reduce waste disposal costs by 30%"
    },
    logistics: {
      "Fleet Management": "Route optimization AI reduces fuel costs by 18% - save ₹5L annually",
      "Warehouse": "Smart lighting systems reduce electricity costs by 40% - save ₹2L annually",
      "Route Planning": "AI route optimization reduces delivery time by 22% and fuel by 18%",
      "Cargo Handling": "Automated cargo systems reduce manual labor costs by 25%",
      "Distribution": "Centralized distribution reduces transport costs by 30%"
    },
    retail: {
      "Store Operations": "Smart HVAC systems reduce energy costs by 30% - save ₹4L annually",
      "Inventory": "AI demand prediction reduces unsold inventory by 35% - save ₹3L annually",
      "Customer Service": "Digital customer support reduces paper forms by 90% - save ₹80K annually",
      "Online Sales": "Energy-efficient servers reduce hosting costs by 40%",
      "Procurement": "Sustainable supplier selection reduces material costs by 15%"
    },
    services: {
      "Operations": "Digital-first client meetings reduce travel emissions by 60% - save ₹1.5L annually",
      "IT": "Cloud migration reduces server energy costs by 45% - save ₹2L annually",
      "Office Management": "Smart building systems reduce utilities by 35% - save ₹2.5L annually",
      "Client Relations": "Digital communication tools reduce travel costs by 50%",
      "Administration": "Paperless office systems save ₹1L annually in printing costs"
    },
    textile: {
      "Weaving": "Energy-efficient looms reduce electricity consumption by 25%",
      "Dyeing": "Water recycling systems reduce water costs by 40% - save ₹3L annually",
      "Cutting": "Automated cutting systems reduce fabric waste by 20%",
      "Stitching": "LED lighting in stitching units reduces energy costs by 50%",
      "Quality Check": "Digital quality systems reduce inspection time by 30%",
      "Finishing": "Steam recovery systems reduce energy costs by 35%"
    },
    food: {
      "Processing": "Energy-efficient processing equipment reduces costs by 30%",
      "Packaging": "Biodegradable packaging reduces disposal costs by 45%",
      "Quality Control": "Automated testing reduces labor costs by 25%",
      "Storage": "Smart cold storage systems reduce energy costs by 40%",
      "Distribution": "Temperature-controlled logistics optimize energy usage by 35%"
    },
    automotive: {
      "Assembly": "Automated assembly lines reduce energy consumption by 25%",
      "Parts Manufacturing": "Precision manufacturing reduces material waste by 30%",
      "Quality Testing": "Digital testing systems reduce inspection costs by 40%",
      "Paint Shop": "Water-based paints reduce environmental costs by 50%",
      "Final Assembly": "Just-in-time assembly reduces inventory costs by 35%"
    },
    chemicals: {
      "Production": "Process optimization reduces raw material waste by 20%",
      "R&D": "Digital labs reduce chemical waste by 35%",
      "Quality Control": "Automated testing reduces sample waste by 40%",
      "Safety": "Smart monitoring systems reduce compliance costs by 30%",
      "Packaging": "Bulk packaging reduces material costs by 25%"
    },
    construction: {
      "Project Management": "Digital project tools reduce paper usage by 85%",
      "Construction": "Modular construction reduces material waste by 30%",
      "Materials": "Recycled materials reduce procurement costs by 20%",
      "Safety": "IoT safety systems reduce accident costs by 45%",
      "Design": "3D modeling reduces design revision costs by 35%"
    },
    agriculture: {
      "Farming": "Precision farming reduces fertilizer usage by 30%",
      "Processing": "Solar drying systems reduce energy costs by 60%",
      "Storage": "Smart storage reduces crop loss by 25%",
      "Distribution": "Cold chain optimization reduces spoilage by 40%",
      "Quality Control": "Digital grading systems improve efficiency by 35%"
    },
    electronics: {
      "Assembly": "Automated assembly reduces defect rates by 30%",
      "Testing": "AI-powered testing reduces testing time by 40%",
      "R&D": "Digital prototyping reduces development costs by 50%",
      "Quality Control": "Computer vision reduces inspection costs by 35%",
      "Packaging": "Anti-static packaging reduces damage by 25%"
    },
    healthcare: {
      "Patient Care": "Digital health records reduce paper costs by 90%",
      "Administration": "Automated billing reduces processing costs by 40%",
      "Equipment": "Predictive maintenance reduces downtime by 35%",
      "Pharmacy": "Automated dispensing reduces errors by 50%",
      "Laboratory": "Digital reports reduce paper usage by 85%"
    },
    education: {
      "Administration": "Digital admissions reduce paper costs by 80%",
      "IT": "Cloud systems reduce server costs by 50%",
      "Facilities": "Smart lighting reduces energy costs by 40%",
      "Student Services": "Digital services reduce processing costs by 35%",
      "Library": "Digital collections reduce space costs by 60%"
    },
    hospitality: {
      "Front Office": "Digital check-in reduces paper usage by 85%",
      "Housekeeping": "Smart room controls reduce energy costs by 30%",
      "Food Service": "Waste tracking reduces food waste by 40%",
      "Maintenance": "Predictive maintenance reduces costs by 35%",
      "Events": "Digital event management reduces planning costs by 50%"
    },
    energy: {
      "Generation": "Smart grid systems improve efficiency by 25%",
      "Distribution": "Smart meters reduce losses by 20%",
      "Maintenance": "Predictive maintenance reduces downtime by 40%",
      "Customer Service": "Digital services reduce operational costs by 35%",
      "Operations": "AI optimization reduces operational costs by 30%"
    }
  };

  const carbonFootprintSuggestions = [
    "Switch to renewable energy sources - reduce CO2 by 40%",
    "Implement paperless operations - save 2 tons CO2 annually",
    "Optimize transportation routes - reduce emissions by 25%",
    "Use energy-efficient equipment - cut carbon footprint by 30%",
    "Promote remote work - decrease commuting emissions by 50%"
  ];

  const energySavingSuggestions = [
    "Install LED lighting systems - 60% energy reduction",
    "Implement smart HVAC controls - 35% cooling cost savings",
    "Use motion sensors for lighting - 40% electricity savings",
    "Upgrade to energy-efficient motors - 25% power reduction",
    "Solar panel installation - 70% renewable energy coverage"
  ];

  const getSuggestion = () => {
    const suggestion = suggestions[selectedEnterprise]?.[selectedDepartment] || "AI is analyzing your selection...";
    setCurrentSuggestion(suggestion);
  };

  const calculateSustainabilityScore = () => {
    const energy = parseInt(inputs.energy) || 0;
    const waste = parseInt(inputs.waste) || 0;
    const transport = parseInt(inputs.transport) || 0;
    const water = parseInt(inputs.water) || 0;
    const employees = parseInt(inputs.employees) || 1;
    
    // AI-based scoring algorithm
    let baseScore = 50;
    
    // Energy efficiency score (0-25 points)
    const energyPerEmployee = energy / employees;
    const energyScore = Math.max(0, 25 - (energyPerEmployee / 100));
    
    // Waste management score (0-25 points)
    const wastePerEmployee = waste / employees;
    const wasteScore = Math.max(0, 25 - (wastePerEmployee / 20));
    
    // Transport efficiency score (0-25 points)
    const transportScore = Math.max(0, 25 - (transport / 200));
    
    // Water usage score (0-25 points)
    const waterPerEmployee = water / employees;
    const waterScore = Math.max(0, 25 - (waterPerEmployee / 50));
    
    const totalScore = Math.min(100, Math.round(energyScore + wasteScore + transportScore + waterScore));
    setSustainabilityScore(totalScore);
  };

  const calculatePotentialSavings = () => {
    const energy = parseInt(inputs.energy) || 0;
    const waste = parseInt(inputs.waste) || 0;
    const transport = parseInt(inputs.transport) || 0;
    
    const energySavings = (energy * 12 * 0.25); // 25% energy cost reduction potential
    const wasteSavings = (waste * 12 * 0.30); // 30% waste cost reduction potential  
    const transportSavings = (transport * 12 * 0.20); // 20% transport cost reduction potential
    
    return Math.round(energySavings + wasteSavings + transportSavings);
  };

  const addReview = () => {
    if (newReview.name && newReview.text) {
      setReviews([...reviews, { ...newReview }]);
      setNewReview({ name: '', company: '', rating: 5, text: '' });
    }
  };

  const tabs = [
    { id: 'suggestions', name: 'AI Suggestions', icon: <Bot className="w-5 h-5" /> },
    { id: 'score', name: 'Sustainability Score', icon: <BarChart3 className="w-5 h-5" /> },
    { id: 'inputs', name: 'Business Inputs', icon: <Building className="w-5 h-5" /> },
    { id: 'reviews', name: 'Reviews', icon: <Star className="w-5 h-5" /> }
  ];

  return (
    <div className="max-w-5xl mx-auto p-6 bg-gray-50 min-h-screen">
      {/* Header */}
      <div className="bg-white rounded-lg shadow p-6 mb-6">
        <h1 className="text-2xl font-bold text-gray-800 mb-2 flex items-center gap-3">
          <Bot className="text-blue-600" />
          MSME Sustainability AI Platform
        </h1>
        <p className="text-gray-600">AI-powered sustainability scoring and cost-saving recommendations</p>
      </div>

      {/* Business Selection */}
      <div className="bg-white rounded-lg shadow p-6 mb-6">
        <h2 className="text-lg font-semibold mb-4">Business Details</h2>
        <div className="grid md:grid-cols-2 gap-6">
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-2">
              Business Type
            </label>
            <select
              value={selectedEnterprise}
              onChange={(e) => {
                setSelectedEnterprise(e.target.value);
                setSelectedDepartment(enterprises[e.target.value].departments[0]);
                setCurrentSuggestion('');
              }}
              className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500"
            >
              <option value="manufacturing">Manufacturing & Production</option>
              <option value="logistics">Logistics & Transportation</option>
              <option value="retail">Retail & E-commerce</option>
              <option value="services">Professional Services</option>
              <option value="textile">Textile & Garments</option>
              <option value="food">Food & Beverage</option>
              <option value="automotive">Automotive & Parts</option>
              <option value="chemicals">Chemicals & Pharmaceuticals</option>
              <option value="construction">Construction & Real Estate</option>
              <option value="agriculture">Agriculture & Agro-processing</option>
              <option value="electronics">Electronics & Technology</option>
              <option value="healthcare">Healthcare & Medical</option>
              <option value="education">Education & Training</option>
              <option value="hospitality">Hospitality & Tourism</option>
              <option value="energy">Energy & Utilities</option>
            </select>
          </div>

          <div>
            <label className="block text-sm font-medium text-gray-700 mb-2">
              Department/Section
            </label>
            <select
              value={selectedDepartment}
              onChange={(e) => {
                setSelectedDepartment(e.target.value);
                setCurrentSuggestion('');
              }}
              className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500"
            >
              {enterprises[selectedEnterprise].departments.map((dept) => (
                <option key={dept} value={dept}>{dept}</option>
              ))}
            </select>
          </div>
        </div>

        <div className="mt-4 p-3 bg-blue-50 border border-blue-200 rounded-lg">
          <p className="text-sm text-blue-700">
            <strong>Selected:</strong> {enterprises[selectedEnterprise].name} → {selectedDepartment}
          </p>
        </div>
      </div>

      {/* Tabs */}
      <div className="bg-white rounded-lg shadow mb-6">
        <div className="border-b border-gray-200">
          <nav className="flex">
            {tabs.map((tab) => (
              <button
                key={tab.id}
                onClick={() => setActiveTab(tab.id)}
                className={`flex items-center gap-2 px-6 py-4 border-b-2 font-medium text-sm transition-all ${
                  activeTab === tab.id
                    ? 'border-blue-500 text-blue-600'
                    : 'border-transparent text-gray-500 hover:text-gray-700'
                }`}
              >
                {tab.icon}
                {tab.name}
              </button>
            ))}
          </nav>
        </div>

        <div className="p-6">
          {/* AI Suggestions Tab */}
          {activeTab === 'suggestions' && (
            <div>
              <div className="mb-6">
                <p className="text-gray-600 mb-3">
                  Selected: <span className="font-medium">{enterprises[selectedEnterprise].name}</span> → 
                  <span className="font-medium"> {selectedDepartment}</span>
                </p>
                
                <button
                  onClick={getSuggestion}
                  className="bg-blue-600 text-white px-6 py-3 rounded-lg hover:bg-blue-700 transition-colors flex items-center gap-2"
                >
                  <Bot className="w-5 h-5" />
                  Get AI Suggestion
                </button>
              </div>

              {currentSuggestion && (
                <div className="mb-6 p-4 bg-blue-50 border border-blue-200 rounded-lg">
                  <div className="flex items-start gap-3">
                    <Lightbulb className="w-5 h-5 text-blue-600 mt-0.5 flex-shrink-0" />
                    <div>
                      <div className="font-medium text-blue-800 mb-1">AI Recommendation:</div>
                      <div className="text-blue-700">{currentSuggestion}</div>
                    </div>
                  </div>
                </div>
              )}

              <div className="grid md:grid-cols-2 gap-6">
                <div>
                  <h3 className="font-semibold text-gray-800 mb-3 flex items-center gap-2">
                    <Leaf className="w-5 h-5 text-green-500" />
                    Carbon Footprint Reduction
                  </h3>
                  <div className="space-y-2">
                    {carbonFootprintSuggestions.map((suggestion, i) => (
                      <div key={i} className="p-3 bg-green-50 border border-green-200 rounded text-sm">
                        🌱 {suggestion}
                      </div>
                    ))}
                  </div>
                </div>

                <div>
                  <h3 className="font-semibold text-gray-800 mb-3 flex items-center gap-2">
                    <Zap className="w-5 h-5 text-yellow-500" />
                    Energy Saving Tips
                  </h3>
                  <div className="space-y-2">
                    {energySavingSuggestions.map((suggestion, i) => (
                      <div key={i} className="p-3 bg-yellow-50 border border-yellow-200 rounded text-sm">
                        ⚡ {suggestion}
                      </div>
                    ))}
                  </div>
                </div>
              </div>
            </div>
          )}

          {/* Sustainability Score Tab */}
          {activeTab === 'score' && (
            <div>
              {sustainabilityScore === 0 ? (
                <div className="text-center py-12">
                  <div className="w-24 h-24 bg-gray-100 rounded-full flex items-center justify-center mx-auto mb-4">
                    <BarChart3 className="w-12 h-12 text-gray-400" />
                  </div>
                  <h3 className="text-xl font-semibold text-gray-800 mb-2">Ready to Calculate Your Score?</h3>
                  <p className="text-gray-600 mb-4">Enter your business data in the "Business Inputs" tab to get your sustainability score</p>
                  <button
                    onClick={() => setActiveTab('inputs')}
                    className="bg-blue-600 text-white px-6 py-3 rounded-lg hover:bg-blue-700 transition-colors"
                  >
                    Enter Business Data
                  </button>
                </div>
              ) : (
                <div>
                  <div className="text-center mb-8">
                    <div className="relative inline-block">
                      <div className="w-40 h-40 rounded-full bg-gradient-to-br from-green-400 to-blue-500 flex items-center justify-center text-white mb-4 relative">
                        <div className="text-center">
                          <div className="text-4xl font-bold">{sustainabilityScore}</div>
                          <div className="text-sm opacity-90">/ 100</div>
                        </div>
                        <div className="absolute -top-2 -right-2">
                          {sustainabilityScore >= 80 ? (
                            <div className="bg-green-500 text-white px-2 py-1 rounded-full text-xs font-bold">Excellent</div>
                          ) : sustainabilityScore >= 60 ? (
                            <div className="bg-yellow-500 text-white px-2 py-1 rounded-full text-xs font-bold">Good</div>
                          ) : sustainabilityScore >= 40 ? (
                            <div className="bg-orange-500 text-white px-2 py-1 rounded-full text-xs font-bold">Fair</div>
                          ) : (
                            <div className="bg-red-500 text-white px-2 py-1 rounded-full text-xs font-bold">Needs Work</div>
                          )}
                        </div>
                      </div>
                    </div>
                    <h3 className="text-2xl font-semibold text-gray-800 mb-2">Your Sustainability Score</h3>
                    <p className="text-gray-600">
                      {sustainabilityScore >= 80 ? "Outstanding! You're a sustainability leader." :
                       sustainabilityScore >= 60 ? "Great work! You're on the right track." :
                       sustainabilityScore >= 40 ? "Good start! There's room for improvement." :
                       "Let's work together to improve your sustainability."}
                    </p>
                  </div>

                  <div className="grid md:grid-cols-2 gap-6 mb-8">
                    <div className="p-6 bg-gradient-to-r from-green-50 to-green-100 border border-green-200 rounded-xl">
                      <div className="flex items-center gap-3 mb-3">
                        <DollarSign className="w-6 h-6 text-green-600" />
                        <h4 className="font-semibold text-green-800">Potential Annual Savings</h4>
                      </div>
                      <div className="text-3xl font-bold text-green-600 mb-2">₹{calculatePotentialSavings().toLocaleString()}</div>
                      <p className="text-sm text-green-700">Based on AI analysis of your current operations</p>
                      <div className="mt-3 text-xs text-green-600">
                        💡 This could pay for sustainability upgrades in 6-12 months!
                      </div>
                    </div>
                    
                    <div className="p-6 bg-gradient-to-r from-blue-50 to-blue-100 border border-blue-200 rounded-xl">
                      <div className="flex items-center gap-3 mb-3">
                        <Leaf className="w-6 h-6 text-blue-600" />
                        <h4 className="font-semibold text-blue-800">Environmental Impact</h4>
                      </div>
                      <div className="space-y-2 text-sm">
                        <div className="flex justify-between">
                          <span>CO2 Reduction Potential:</span>
                          <span className="font-medium text-blue-700">{Math.round(sustainabilityScore * 0.5)}%</span>
                        </div>
                        <div className="flex justify-between">
                          <span>Energy Savings:</span>
                          <span className="font-medium text-blue-700">{Math.round(sustainabilityScore * 0.4)}%</span>
                        </div>
                        <div className="flex justify-between">
                          <span>Waste Reduction:</span>
                          <span className="font-medium text-blue-700">{Math.round(sustainabilityScore * 0.3)}%</span>
                        </div>
                      </div>
                    </div>
                  </div>

                  <div className="bg-white border border-gray-200 rounded-xl p-6">
                    <h4 className="font-semibold text-gray-800 mb-4 flex items-center gap-2">
                      <BarChart3 className="w-5 h-5 text-purple-600" />
                      Score Breakdown
                    </h4>
                    <div className="space-y-4">
                      {[
                        { name: 'Energy Efficiency', score: Math.min(25, Math.round((parseInt(inputs.energy) || 0) > 0 ? Math.max(5, 25 - ((parseInt(inputs.energy) || 0) / (parseInt(inputs.employees) || 1)) / 100) : 0)), color: 'bg-yellow-400' },
                        { name: 'Waste Management', score: Math.min(25, Math.round((parseInt(inputs.waste) || 0) > 0 ? Math.max(5, 25 - ((parseInt(inputs.waste) || 0) / (parseInt(inputs.employees) || 1)) / 20) : 0)), color: 'bg-green-400' },
                        { name: 'Transport Efficiency', score: Math.min(25, Math.round((parseInt(inputs.transport) || 0) > 0 ? Math.max(5, 25 - (parseInt(inputs.transport) || 0) / 200) : 0)), color: 'bg-blue-400' },
                        { name: 'Water Usage', score: Math.min(25, Math.round((parseInt(inputs.water) || 0) > 0 ? Math.max(5, 25 - ((parseInt(inputs.water) || 0) / (parseInt(inputs.employees) || 1)) / 50) : 0)), color: 'bg-purple-400' }
                      ].map((category, i) => (
                        <div key={i} className="space-y-2">
                          <div className="flex justify-between items-center">
                            <span className="font-medium text-gray-700">{category.name}</span>
                            <span className="text-sm font-semibold text-gray-800">{category.score}/25</span>
                          </div>
                          <div className="w-full bg-gray-200 rounded-full h-3">
                            <div
                              className={`h-3 rounded-full transition-all duration-500 ${category.color}`}
                              style={{ width: `${(category.score / 25) * 100}%` }}
                            ></div>
                          </div>
                          <div className="text-xs text-gray-500">
                            {category.score >= 20 ? "Excellent performance" :
                             category.score >= 15 ? "Good, room for improvement" :
                             category.score >= 10 ? "Fair, needs attention" :
                             "Significant improvement needed"}
                          </div>
                        </div>
                      ))}
                    </div>
                  </div>

                  <div className="mt-6 text-center">
                    <button
                      onClick={() => setActiveTab('suggestions')}
                      className="bg-gradient-to-r from-green-500 to-blue-500 text-white px-8 py-3 rounded-lg hover:from-green-600 hover:to-blue-600 transition-all flex items-center gap-2 mx-auto"
                    >
                      <Lightbulb className="w-5 h-5" />
                      Get AI Improvement Suggestions
                    </button>
                  </div>
                </div>
              )}
            </div>
          )}

          {/* Business Inputs Tab */}
          {activeTab === 'inputs' && (
            <div>
              <div className="bg-blue-50 border border-blue-200 rounded-lg p-4 mb-6">
                <h3 className="font-semibold text-blue-800 mb-2 flex items-center gap-2">
                  <Lightbulb className="w-5 h-5" />
                  How it works
                </h3>
                <p className="text-sm text-blue-700">
                  Enter your monthly costs below. Our AI will analyze your data and calculate a sustainability score from 0-100, 
                  plus show you exactly how much money you can save through eco-friendly improvements.
                </p>
              </div>

              <div className="grid md:grid-cols-2 gap-8">
                <div className="space-y-6">
                  <h4 className="font-semibold text-gray-800 border-b border-gray-200 pb-2">Monthly Operating Costs</h4>
                  
                  <div className="space-y-4">
                    <div>
                      <label className="block text-sm font-medium text-gray-700 mb-2 flex items-center gap-2">
                        <Zap className="w-4 h-4 text-yellow-500" />
                        Electricity & Energy Cost (₹/month)
                      </label>
                      <input
                        type="number"
                        value={inputs.energy}
                        onChange={(e) => setInputs({...inputs, energy: e.target.value})}
                        className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 text-lg"
                        placeholder="e.g., 50,000"
                      />
                      <p className="text-xs text-gray-500 mt-1">Include electricity bills, generator fuel, etc.</p>
                    </div>
                    
                    <div>
                      <label className="block text-sm font-medium text-gray-700 mb-2 flex items-center gap-2">
                        <Package className="w-4 h-4 text-green-500" />
                        Waste Disposal Cost (₹/month)
                      </label>
                      <input
                        type="number"
                        value={inputs.waste}
                        onChange={(e) => setInputs({...inputs, waste: e.target.value})}
                        className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 text-lg"
                        placeholder="e.g., 15,000"
                      />
                      <p className="text-xs text-gray-500 mt-1">Garbage collection, recycling, disposal fees</p>
                    </div>

                    <div>
                      <label className="block text-sm font-medium text-gray-700 mb-2 flex items-center gap-2">
                        <Truck className="w-4 h-4 text-blue-500" />
                        Transport & Logistics Cost (₹/month)
                      </label>
                      <input
                        type="number"
                        value={inputs.transport}
                        onChange={(e) => setInputs({...inputs, transport: e.target.value})}
                        className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 text-lg"
                        placeholder="e.g., 30,000"
                      />
                      <p className="text-xs text-gray-500 mt-1">Fuel, vehicle maintenance, delivery costs</p>
                    </div>

                    <div>
                      <label className="block text-sm font-medium text-gray-700 mb-2 flex items-center gap-2">
                        💧
                        Water & Utilities Cost (₹/month)
                      </label>
                      <input
                        type="number"
                        value={inputs.water}
                        onChange={(e) => setInputs({...inputs, water: e.target.value})}
                        className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 text-lg"
                        placeholder="e.g., 8,000"
                      />
                      <p className="text-xs text-gray-500 mt-1">Water bills, sewage, utility connections</p>
                    </div>

                    <div>
                      <label className="block text-sm font-medium text-gray-700 mb-2 flex items-center gap-2">
                        <Users className="w-4 h-4 text-purple-500" />
                        Number of Employees
                      </label>
                      <input
                        type="number"
                        value={inputs.employees}
                        onChange={(e) => setInputs({...inputs, employees: e.target.value})}
                        className="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 text-lg"
                        placeholder="e.g., 25"
                      />
                      <p className="text-xs text-gray-500 mt-1">Total full-time equivalent employees</p>
                    </div>
                  </div>
                </div>

                <div className="space-y-6">
                  <h4 className="font-semibold text-gray-800 border-b border-gray-200 pb-2">AI Analysis Preview</h4>
                  
                  {Object.values(inputs).some(val => val) ? (
                    <div className="space-y-4">
                      <div className="p-4 bg-yellow-50 border border-yellow-200 rounded-lg">
                        <h5 className="font-medium text-yellow-800 mb-2">📊 Data Analysis</h5>
                        <div className="text-sm space-y-1">
                          {inputs.energy && <div>⚡ Energy cost per employee: ₹{Math.round((parseInt(inputs.energy) || 0) / (parseInt(inputs.employees) || 1)).toLocaleString()}/month</div>}
                          {inputs.waste && <div>🗑️ Waste cost per employee: ₹{Math.round((parseInt(inputs.waste) || 0) / (parseInt(inputs.employees) || 1)).toLocaleString()}/month</div>}
                          {inputs.transport && <div>🚛 Transport cost: ₹{parseInt(inputs.transport).toLocaleString()}/month</div>}
                          {inputs.water && <div>💧 Water cost per employee: ₹{Math.round((parseInt(inputs.water) || 0) / (parseInt(inputs.employees) || 1)).toLocaleString()}/month</div>}
                        </div>
                      </div>

                      <div className="p-4 bg-green-50 border border-green-200 rounded-lg">
                        <h5 className="font-medium text-green-800 mb-2">💰 Estimated Savings Potential</h5>
                        <div className="text-sm space-y-1">
                          {inputs.energy && <div>⚡ Energy: ₹{Math.round((parseInt(inputs.energy) || 0) * 12 * 0.25).toLocaleString()}/year (25% reduction possible)</div>}
                          {inputs.waste && <div>🗑️ Waste: ₹{Math.round((parseInt(inputs.waste) || 0) * 12 * 0.30).toLocaleString()}/year (30% reduction possible)</div>}
                          {inputs.transport && <div>🚛 Transport: ₹{Math.round((parseInt(inputs.transport) || 0) * 12 * 0.20).toLocaleString()}/year (20% reduction possible)</div>}
                          {inputs.water && <div>💧 Water: ₹{Math.round((parseInt(inputs.water) || 0) * 12 * 0.15).toLocaleString()}/year (15% reduction possible)</div>}
                        </div>
                      </div>

                      <button
                        onClick={calculateSustainabilityScore}
                        className="w-full bg-gradient-to-r from-green-500 to-blue-500 text-white px-6 py-4 rounded-lg hover:from-green-600 hover:to-blue-600 transition-all flex items-center justify-center gap-2 text-lg font-medium"
                      >
                        <BarChart3 className="w-6 h-6" />
                        Calculate My AI Score
                      </button>

                      {sustainabilityScore > 0 && (
                        <div className="text-center">
                          <button
                            onClick={() => setActiveTab('score')}
                            className="text-blue-600 hover:text-blue-700 font-medium flex items-center gap-2 mx-auto"
                          >
                            View My Score <span className="text-2xl">→</span>
                          </button>
                        </div>
                      )}
                    </div>
                  ) : (
                    <div className="text-center py-8">
                      <div className="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mx-auto mb-4">
                        <BarChart3 className="w-8 h-8 text-gray-400" />
                      </div>
                      <h5 className="font-medium text-gray-600 mb-2">Ready for Analysis</h5>
                      <p className="text-sm text-gray-500">
                        Start entering your costs to see real-time AI insights and savings potential
                      </p>
                    </div>
                  )}
                </div>
              </div>
            </div>
          )}

          {/* Reviews Tab */}
          {activeTab === 'reviews' && (
            <div>
              <h3 className="text-lg font-semibold mb-4">Customer Reviews</h3>
              
              <div className="grid md:grid-cols-2 gap-6">
                <div>
                  <h4 className="font-medium mb-3">Recent Reviews</h4>
                  <div className="space-y-4">
                    {reviews.map((review, i) => (
                      <div key={i} className="p-4 border border-gray-200 rounded-lg">
                        <div className="flex items-center gap-2 mb-2">
                          <div className="font-medium text-sm">{review.name}</div>
                          <div className="text-xs text-gray-500">- {review.company}</div>
                          <div className="flex text-yellow-400 ml-auto">
                            {[...Array(review.rating)].map((_, i) => (
                              <Star key={i} className="w-4 h-4 fill-current" />
                            ))}
                          </div>
                        </div>
                        <p className="text-sm text-gray-600">{review.text}</p>
                      </div>
                    ))}
                  </div>
                </div>

                <div>
                  <h4 className="font-medium mb-3">Add Your Review</h4>
                  <div className="space-y-3">
                    <input
                      type="text"
                      placeholder="Your Name"
                      value={newReview.name}
                      onChange={(e) => setNewReview({...newReview, name: e.target.value})}
                      className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500"
                    />
                    
                    <input
                      type="text"
                      placeholder="Company Name"
                      value={newReview.company}
                      onChange={(e) => setNewReview({...newReview, company: e.target.value})}
                      className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500"
                    />

                    <select
                      value={newReview.rating}
                      onChange={(e) => setNewReview({...newReview, rating: parseInt(e.target.value)})}
                      className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500"
                    >
                      <option value={5}>5 Stars</option>
                      <option value={4}>4 Stars</option>
                      <option value={3}>3 Stars</option>
                      <option value={2}>2 Stars</option>
                      <option value={1}>1 Star</option>
                    </select>

                    <textarea
                      placeholder="Write your review..."
                      value={newReview.text}
                      onChange={(e) => setNewReview({...newReview, text: e.target.value})}
                      className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500 h-20"
                    />

                    <button
                      onClick={addReview}
                      className="w-full bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors"
                    >
                      Add Review
                    </button>
                  </div>
                </div>
              </div>
            </div>
          )}
        </div>
      </div>

      {/* Simple Stats */}
      <div className="grid grid-cols-1 md:grid-cols-4 gap-4">
        <div className="bg-white rounded-lg shadow p-4 text-center">
          <BarChart3 className="w-8 h-8 text-blue-600 mx-auto mb-2" />
          <div className="font-medium">AI Scoring</div>
          <div className="text-sm text-gray-600">Real-time calculation</div>
        </div>
        <div className="bg-white rounded-lg shadow p-4 text-center">
          <Leaf className="w-8 h-8 text-green-600 mx-auto mb-2" />
          <div className="font-medium">Carbon Reduction</div>
          <div className="text-sm text-gray-600">Up to 40% decrease</div>
        </div>
        <div className="bg-white rounded-lg shadow p-4 text-center">
          <DollarSign className="w-8 h-8 text-purple-600 mx-auto mb-2" />
          <div className="font-medium">Cost Savings</div>
          <div className="text-sm text-gray-600">₹1-7L+ annually</div>
        </div>
        <div className="bg-white rounded-lg shadow p-4 text-center">
          <Users className="w-8 h-8 text-orange-600 mx-auto mb-2" />
          <div className="font-medium">Happy Customers</div>
          <div className="text-sm text-gray-600">500+ MSMEs served</div>
        </div>
      </div>
    </div>
  );
};

export default CustomerJourney;
# hackathon
